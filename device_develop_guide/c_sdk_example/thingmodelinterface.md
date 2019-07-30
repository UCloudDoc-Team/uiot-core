
# 设备物模型开发

UIoT-Core 通过物模型功能简化用户应用程序的开发。本章描述如何利用设备端 C-SDK 提供的 API 进行设备端的物模型开发。下面的讲解对应于 C-SDK 示例代码 samples/dev_model/dev_model_sample.c

## 功能说明

* C-SDK 支持物模型七种消息类型，对应于 uiot_export_dm.h 中枚举类型 DM_Type

  ```C
  typedef enum _dm_type {
      PROPERTY_RESTORE,         //设备恢复属性
      PROPERTY_POST,            //设备上报属性
      PROPERTY_SET,             //云端下发属性
      PROPERTY_DESIRED_GET,     //设备获取desire属性
      PROPERTY_DESIRED_DELETE,  //删除云端desire属性
      EVENT_POST,               //设备上报事件
      COMMAND,                  //命令下发
      DM_TYPE_MAX
  }DM_Type;
  ```

  示例代码展示其中设备上报属性、云端下发属性、设备上报事件、命令下发四种操作。

* 目前用户需要根据物模型定义自行装配及解析部分 Json 消息，具体格式可参照物模型消息协议。

## 开发步骤

### 场景

示例代码基于一个”智能音箱“的场景，分别定义了一个”音量“属性，一个”低电量告警“事件，以及一个”下载音乐“命令。具体的物模型 json 文档如下所示：

```json
{
  "Property": [
    {
      "PropertyID": 82,
      "Identifier": "volume",
      "Name": "音量",
      "AccessMode": "rw",
      "Description": "智能音箱音量，数值表示音量百分比",
      "DataType": {
        "Type": "int32",
        "Spec": {
          "Max": 100,
          "Min": 0,
          "Step": 1,
          "UnitName": ""
        }
      }
    }
  ],
  "Event": [
    {
      "EventID": 39,
      "Identifier": "low_power_alert",
      "Name": "低电量告警",
      "Type": "warning",
      "Description": "当电量小于10%触发低电量告警",
      "Output": [
        {
          "Identifier": "power",
          "Name": "电量百分比",
          "DataType": {
            "Type": "int32",
            "Spec": {
              "Max": 10,
              "Min": 0,
              "Step": 1,
              "UnitName": ""
            }
          }
        }
      ]
    }
  ],
  "Command": [
    {
      "CommandID": 47,
      "Identifier": "download_music",
      "Name": "下载音乐",
      "Description": "控制智能音箱从指定URL下载音乐资源",
      "Input": [
        {
          "Identifier": "url",
          "Name": "音乐资源URL",
          "DataType": {
            "Type": "string",
            "Spec": {
              "Length": 255
            }
          }
        }
      ],
      "Output": [
        {
          "Identifier": "result",
          "Name": "执行结果",
          "DataType": {
            "Type": "bool",
            "Spec": {
              "0": "执行失败",
              "1": "执行成功"
            }
          }
        }
      ]
    }
  ]
}
```

用户可参考控制台操作指南，在控制台添加上述物模型功能定义（ID可能会有所差异，但不影响）。创建完成后，替换示例代码中的设备四元组信息。

### 初始化

在使用设备物模型功能之前，首先需要进行初始化，包括 MQTT 客户端的创建和物模型功能的初始化。可参照 dev_model_sample.c 中 main 函数的初始化部分代码。

```C
//1. 首先创建 MQTT 客户端，并与云端建立MQTT连接
void *client = IOT_MQTT_Construct(&init_params);
if (client != NULL) {
    LOG_INFO("Cloud Device Construct Success");
} else {
    LOG_ERROR("Cloud Device Construct Failed");
    return FAILURE;
}
IOT_MQTT_Yield(client, 50);

//2. 初始化设备物模型，获取句柄
void *h_dm = IOT_DM_Init(UIOT_MY_PRODUCT_SN, UIOT_MY_DEVICE_SN, client);
if (NULL == h_dm) {
    LOG_ERROR("initialize device model failed");
    return FAILURE;
}
IOT_DM_Yield(h_dm, 50);
```

### 设备上报属性

用户可使用 API 函数 `IOT_DM_Property_Report` 进行属性上报。如果需要接收上报响应消息，利用 `IOT_DM_RegisterCallback` 注册对应的回调函数。

```C
//根据 uiot_export_dm.h 中的声明，定义属性上报的回调函数，获取属性上报的响应。
int property_post_cb(const char *request_id, const int ret_code){
    LOG_INFO("property_post_cb; request_id: %s; ret_code: %d", request_id, ret_code)
    return SUCCESS;
}

int main(int argc, char **argv)
{
    ...
    //注册回调函数
    IOT_DM_RegisterCallback(PROPERTY_POST , h_dm, property_post_cb);
    ...
    for (int i = 0; i < 10; i++) {
        //属性上报
        IOT_DM_Property_Report(h_dm, PROPERTY_POST, i * 2, "{\"volume\": {\"Value\":50}}");
        ...
        IOT_DM_Yield(h_dm, 200);
        HAL_SleepMs(2000);
    }
    ...
}
```

### 云端下发属性

利用 `IOT_DM_RegisterCallback` 注册对应的回调函数，接收云端下发的属性值。

```C
//根据 uiot_export_dm.h 中的声明，定义属性下发的回调函数，获取云端下发的属性值。实际应用中可在该回调函数中处理下发的属性值
int property_set_cb(const char *request_id, const char *property){
    LOG_INFO("property_set_cb; request_id: %s; property: %s", request_id, property)
    return SUCCESS;
}

int main(int argc, char **argv)
{
    ...
    //注册回调函数
    IOT_DM_RegisterCallback(PROPERTY_SET , h_dm, property_set_cb);
    ...
}
```

### 设备上报事件

用户可使用 API 函数 `IOT_DM_TriggerEvent` 进行事件上报。如果需要接收上报响应消息，利用 `IOT_DM_RegisterCallback` 注册对应的回调函数。

```C
//根据 uiot_export_dm.h 中的声明，定义事件上报的回调函数，获取事件上报的响应。
int event_post_cb(const char *request_id, const int ret_code){
    LOG_INFO("event_post_cb; request_id: %s; ret_code: %d", request_id, ret_code)
    return SUCCESS;
}

int main(int argc, char **argv)
{
    ...
    //注册回调函数
    IOT_DM_RegisterCallback(EVENT_POST, h_dm, event_post_cb);
    ...
    for (int i = 0; i < 10; i++) {
        //事件上报
        IOT_DM_TriggerEvent(h_dm, i * 2 + 1, "low_power_alert", "{\"power\": 5}");
        ...
        IOT_DM_Yield(h_dm, 200);
        HAL_SleepMs(2000);
    }
    ...
}
```

### 命令下发

利用 `IOT_DM_RegisterCallback` 注册对应的回调函数，接收云端下发的命令。

```C
//根据 uiot_export_dm.h 中的声明，定义命令下发的回调函数，获取云端下发的命令。实际应用中可在该回调函数中处理命令的输入输出
int command_cb(const char *request_id, const char *identifier, const char *input, char **output){
    LOG_INFO("command_cb; request_id: %s; identifier: %s; input: %s", request_id, identifier, input)
    *output = (char *)HAL_Malloc(100);
    HAL_Snprintf(*output, 1000, "{\"result\":%d}", 1);
    return SUCCESS;
}

int main(int argc, char **argv)
{
    ...
    //注册回调函数
    IOT_DM_RegisterCallback(COMMAND , h_dm, command_cb);
    ...
}
```

注意：在命令的回调函数中，需要用 HAL_Malloc 为 *output 申请内存，并且无需释放，由 SDK 负责释放该内存空间。

### 资源释放

```C
//释放物模型资源
IOT_DM_Destroy(h_dm);
//（可选）释放 MQTT Client 资源
IOT_MQTT_Destroy(&client);
```

## API 列表

### IOT_DM_RegisterCallback

注册消息回调函数的宏

```C
#define IOT_DM_RegisterCallback(type, handle, cb)
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| type | DM_Type | 输入 | 消息类型，七种DM_Type之一 |
| handle | void * | 输入 | IOT_DM_Init 返回的句柄 |
| cb | 函数指针 | 输入 | 回调函数指针，函数类型必须与 DECLARE_DM_CALLBACK 声明的类型相同 |
| ret | int | 返回值 | <0: 注册消息回调函数失败<br> =0: 注册消息回调函数成功 |

### IOT_DM_Init

初始化设备物模型

```C
void *IOT_DM_Init(const char *product_sn, const char *device_sn, void *ch_signal);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| product_sn | const char * | 输入 | 指向产品序列号的指针 |
| device_sn | const char * | 输入 | 指向设备序列号的指针 |
| ch_signal | void * | 输入 | 指定的信号通道，目前为 IOT_MQTT_Construct 返回的句柄 |
| ret | void * | 返回值 | 初始化成功，返回句柄；初始化失败，返回 NULL |

### IOT_DM_Destroy

释放设备物模型相关的资源

```C
int IOT_DM_Destroy(void *handle);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_DM_Init 返回的句柄 |
| ret | int | 返回值 | <0: 失败<br> =0: 成功 |

### IOT_DM_Property_Report

属性有关的消息上报

```C
int IOT_DM_Property_Report(void *handle, DM_Type type, int request_id, const char *payload);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_DM_Init 返回的句柄 |
| type | DM_Type | 输入 | 消息类型，PROPERTY_RESTORE, PROPERTY_POST, PROPERTY_DESIRED_GET, PROPERTY_DESIRED_DELETE 四种属性相关的消息类型之一 |
| request_id | int | 输入 | 消息的 request_id，由用户决定，用于区分每次属性上报 |
| payload | const char * | 输入 | 消息体 |
| ret | int | 返回值 | <0: 上报失败<br> =0: 上报成功 |

### IOT_DM_TriggerEvent

事件消息上报

```C
int IOT_DM_TriggerEvent(void *handle, int request_id, const char *identifier, const char *payload);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_DM_Init 返回的句柄 |
| request_id | int | 输入 | 消息的 request_id，由用户决定，用于区分不同事件 |
| identifier | const char * | 输入 | 事件的 identifier |
| payload | const char * | 输入 | 消息体 |
| ret | int | 返回值 | <0: 上报失败<br> =0: 上报成功 |

### IOT_DM_Yield

在当前线程为底层 MQTT 客户端让出一定 CPU 执行时间，让其接收网络报文并将消息分发到用户的回调函数中

```C
int IOT_DM_Yield(void *handle, uint32_t timeout_ms);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_DM_Init 返回的句柄 |
| timeout_ms | uint32_t | 输入 | 超时时间，单位：ms |
| ret | int | 返回值 | <0: 失败<br> =0: 成功 |
