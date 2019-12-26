# C-SDK 快速入门

本章描述如何在 linux 环境，通过设备端 C-SDK 快速接入 UIoT-Core 平台服务。

本例通过自定义上行、下行Topic，以及规则引擎的M2M功能，将设备上行数据直接转发到同一设备的下行Topic。

## 准备开发环境

* 操作系统：`linux`
* 必备软件：`make`, `gcc`, `git`, `cmake`


Ubuntu下可使用如下命令安装必备软件：

```
sudo apt-get install -y build-essential make git gcc
```

CentOS下可使用如下命令安装必备软件：

```
sudo yum install -y git make gcc
```

## 获取 C-SDK

* [GitHub](https://github.com/ucloud/ucloud-iot-device-sdk-c)

```
git clone https://github.com/ucloud/ucloud-iot-device-sdk-c
```
## 编译及运行

C-SDK支持 `GNU Make` 构建，开发者可以选择自己熟悉的编译。

### GNU Make

1. 通过修改 C-SDK 顶层目录下的 make.settings 文件，配置开启或者关闭特定功能模块

```
// 本例仅使用消息上下行收发，所以关闭其他模块
FEATURE_MQTT_COMM_ENABLED               = y     # 是否打开MQTT通道
FEATURE_DEVICE_SHADOW_ENABLED           = n     # 是否打开设备影子
FEATURE_OTA_ENABLED                     = n     # 是否打开OTA固件升级
FEATURE_DEVICE_MODEL_ENABLED            = n     # 是否打开物模型
FEATURE_FILE_UPLOAD_ENABLED             = n     # 是否打开文件上传

FEATURE_AUTH_MODE_DYNAMIC               = n     # 是否使能设备动态注册
FEATURE_SUPPORT_TLS                     = y     # 是否打开TLS支持
FEATURE_SDK_TESTS_ENABLED               = n     # 是否打开SDK测试用例编译
```

2. 在SDK顶层目录运行如下命令:

```
make clean
make
```

3. 编译完成后, 生成的可执行文件在当前目录的 output/release/bin目录下


## 基于C-SDK实现基本功能----消息收发

本例结合示例代码讲解如何使用C-SDK的`./samples/mqtt/mqtt_sample.c`实现消息的收发功能：

* 定时向云平台上报消息`{"test": ${num}}`
* 配置规则引擎转发到下行Topic
* 详细代码及main函数参考：`./samples/mqtt/mqtt_sample.c`


**注：以下所有路径均是基于SDK根目录展开**


### 移植步骤

1. 基于使用的OS(linux)的实现HAL层接口

HAL层是对不同操作系统的抽象，HAL层适配了不同操作系统关于线程、内存、Timer、TCP的操作。UCloud IoT C-SDK已经实现了linux、FreeRTOS、RT-Thread下的HAL层实现。


本例移植平台OS为linux，该步已经官方实现，用户可以直接跳过。

示例：HAL接口HAL_Printf：`./platform/os/linux/HAL_OS_linux.c`。

```
  void HAL_Printf(_IN_ const char *fmt, ...)
  {    
  	va_list args;    
  	va_start(args, fmt);    
  	vprintf(fmt, args);    
  	va_end(args);    
  	fflush(stdout);
  }
```

其他接口及OS的HAL层实现代码目录参考：`./platform/os`

2. 获取产品序列号、设备序列号、设备密钥，修改代码中对应的宏定义。

1) 参考[设备详情](/iot/uiot-core/console_guide/product_device/create_devcies#设备详情)获取设备三要素；

![](/images/csdk快速入门获取三要素.png)



2) 通过三要素通过[静态注册](/iot/uiot-core/device_develop_guide/authenticate_devices/unique-certificate-per-device_authentication)接入到UIoT-Core

修改`./samples/mqtt/mqtt_sample.c`中对应的宏。

```
  // 接入UIoT-Core三要素（需要根据控制台信息修改）
  #define UIOT_MY_PRODUCT_SN            "6yggf1so12ex2ska"
  #define UIOT_MY_DEVICE_SN             "00:12:13:14:15:16"
  #define UIOT_MY_DEVICE_SECRET         "qnom9gil9h59x96s"
```

3. main函数详解

- 创建MQTT连接:`IOT_MQTT_Construct`
```
  ret = _setup_connect_init_params(&sg_initParams);    
  if(ret != SUCCESS)    
  {        
  	HAL_Printf("_setup_connect_init_params fail:%d\n", ret);        
  	return ret;    
  }        
  
  void *mqtt_client = IOT_MQTT_Construct(&sg_initParams);    
  if(mqtt_client == NULL)    
  {        
  	HAL_Printf("IOT_MQTT_Construct fail\n");        
  	return ERR_PARAM_INVALID;    
  }        
```

- 订阅下行Topic：`_register_subscribe_topics`

```
    rc = _register_subscribe_topics(client);
    if (rc < 0) {
        HAL_Printf("Client Subscribe Topic Failed: %d", rc);
        return rc;
    }

```

- 周期性上报消息：`_publish_msg`

```
    do {
        // 判断订阅是否成功
        if (sg_sub_packet_id > 0) {
            rc = _publish_msg(client);
            if (rc < 0) {
                HAL_Printf("client publish topic failed :%d.", rc);
            }
        }
        rc = IOT_MQTT_Yield(client, 2000);
    } while (1);

```

4. 修改需要订阅的Topic及收到消息的回调函数

1) 参考[Topic主题管理](/iot/uiot-core/console_guide/product_device/topic)，创建自定义Topic。

默认创建产品时，系统会生成两个分别具有订阅和发布权限的Topic。

|Topic| 权限|描述|
|---|---|---|
|/${ProductSN}/${DeviceSN}/upload|发布|自定义上行Topic|
|/${ProductSN}/${DeviceSN}/set |订阅|自定义下行Topic|

![默认自定义Topic](/images/默认自定义Topic.png)

2) 修改`./samples/mqtt/mqtt_sample.c`中 下行消息的Topic

```
// 订阅下行topic并注册回调函数

static int _register_subscribe_topics(void *client)
{
    static char topic_name[128] = {0};
	
	// 订阅的Topic：/${ProductSN}/${DeviceSN}/set
    int size = HAL_Snprintf(topic_name, sizeof(topic_name), "/%s/%s/%s", UIOT_MY_PRODUCT_SN, UIOT_MY_DEVICE_SN, "set");
    if (size < 0 || size > sizeof(topic_name) - 1)
    {
        HAL_Printf("topic content length not enough! content size:%d  buf size:%d\n", size, (int)sizeof(topic_name));
        return FAILURE_RET;
    }
    SubscribeParams sub_params = DEFAULT_SUB_PARAMS;
	// 注册回调函数
    sub_params.on_message_handler = on_message_callback;
    return IOT_MQTT_Subscribe(client, topic_name, &sub_params);
}

......

// 回调函数，这里将收到的消息打印出来
static void on_message_callback(void *pClient, MQTTMessage *message, void *userData) {
    if (message == NULL) {
            return;
    }

    HAL_Printf("Receive Message With topicName:%.*s, payload:%.*s\n",
                  (int) message->topic_len, message->topic, (int) message->payload_len, (char *) message->payload);
}

```

3) 修改`./samples/mqtt/mqtt_sample.c`中 上行发送的Topic

```
// 发布消息到上行Topic
static int _publish_msg(void *client)
{
    char topicName[128] = {0};
	// 发布消息的Topic：/${ProductSN}/${DeviceSN}/upload
    HAL_Snprintf(topicName, 128, "/%s/%s/%s", UIOT_MY_PRODUCT_SN, UIOT_MY_DEVICE_SN, "upload");

    PublishParams pub_params = DEFAULT_PUB_PARAMS;
    pub_params.qos = QOS1;

    char topic_content[MAX_SIZE_OF_TOPIC_CONTENT + 1] = {0};

    // 发送消息内容：{"test": num}
    int size = HAL_Snprintf(topic_content, sizeof(topic_content), "{\"test\": \"%d\"}", sg_count++);
    if (size < 0 || size > sizeof(topic_content) - 1)
    {
            HAL_Printf("payload content length not enough! content size:%d  buf size:%d\n", size, (int)sizeof(topic_content));
            return -3;
    }

    pub_params.payload = topic_content;
    pub_params.payload_len = strlen(topic_content);

    return IOT_MQTT_Publish(client, topicName, &pub_params);
}

```

4) 保存


5. 配置规则引擎，做M2M转发

参考[数据流转到其他Topic](/iot/uiot-core/console_guide/ruleengine/forward_data_to_topic)，将上行消息转发到下行Topic，并启用规则。

![C-SDK转发Topic](/images/C-SDK转发Topic.png)



### 执行结果

1. 编译及运行

```
// 编译生成可执行文件
make

// 运行
./output/release/bin/mqtt_sample
```

2. 控制台收发结果打印


![控制台收发结果打印](/images/控制台收发结果打印.png)



## 查看日志

通过日志可以看到一段时间内设备所有的上行和下行消息。

![](/images/快速入门查看日志上行.png)

![](/images/快速入门查看日志下行.png)
