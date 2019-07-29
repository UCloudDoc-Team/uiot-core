
# MQTT协议说明 
目前物联网通信支持MQTT标准协议接入（兼容3.1.1版本协议），具体的协议请参考MQTT 3.1.1协议文档 

## 和标准MQTT区别 
1. 支持 MQTT 的 PUB、SUB、PING、PONG、CONNECT、DISCONNECT、UNSUB 等报文。 
2. 支持 cleanSession。 
3. 不支持 will、retain msg。 
4. 不支持 QOS2。 

## MQTT通道，安全等级 
支持TLS协议建立安全连接，保证通信内容安全性。

# 设备身份认证
设备身份认证分为动态认证和静态认证两种。

## 动态认证
动态认证即一型一密，需要打开CMakeLists文件中的ENABLE_FEATURE_AUTH_MODE_DYNAMIC编译开关，提前在设备上烧写ProductSN、DeviceSN、ProductSecret，<br>
通过HAL层的接口获取设备信息，填入MQTT的初始连接参数中，向物联网平台进行动态身份认证，动态认证后部分权限受限需要获取设备密钥后接着进行静态认证。

![](https://i.loli.net/2019/07/18/5d30423caa2fd24915.png)

## 动态认证的函数调用流程图示 

![](https://i.loli.net/2019/07/18/5d30454b6ebb641211.jpg)

## 静态认证
静态认证即一机一密，相比一型一密的安全性比较高，推荐使用，提前在设备上烧写ProductSN、DeviceSN、DeviceSecret，<br>
通过HAL层的接口获取设备信息，填入MQTT的初始连接参数中，向物联网平台进行身份认证。

# MQTT接口说明

## IOT_MQTT_Construct

创建MQTT连接句柄

```C
void *IOT_MQTT_Construct(MQTTInitParams *pParams);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pParams | MQTTInitParams * | 输入 | 创建MQTT连接的参数 |
| ret | void * | 返回 | MQTT的句柄 |

## IOT_MQTT_Destroy

销毁MQTT连接句柄。

```C
void IOT_MQTT_Destroy(void **pClient);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pClient | void ** | 输入 | 指向MQTT句柄的指针 |

## IOT_MQTT_Yield

MQTT会话阶段,MQTT主循环函数, 内含了心跳的维持, 服务器下行报文的收取等

```C
int IOT_MQTT_Yield(void *pClient, uint32_t timeout_ms)
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pClient | void ** | 输入 | 指向MQTT句柄的指针 |
| timeout_ms | uint32_t | 输入 | 等待时间，单位是ms |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_MQTT_Publish

MQTT连接后,向指定topic发送消息。

```C
int IOT_MQTT_Publish(void *pClient, char *topicName, PublishParams *pParams);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pClient | void * | 输入 | MQTT句柄 |
| topicName | char * | 输入 | 发送消息的topic名称 |
| pParams | PublishParams * | 输入 | 发送消息的内容和相关参数 |
| ret | int | 返回 | 发送成功返回packet_id,<br>FAILURE表示失败 |

## IOT_MQTT_Subscribe

MQTT连接后,订阅指定topic。

```C
int IOT_MQTT_Subscribe(void *pClient, char *topicFilter, SubscribeParams *pParams);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pClient| void * | 输入 | MQTT句柄 |
| topicFilter | char * | 输入 | 主题过滤器 |
| pParams | SubscribeParams * | 输入 | 订阅topic的服务质量,回调函数等参数 |
| ret | int | 返回 | 订阅成功返回packet_id,<br>FAILURE表示失败 |

## IOT_MQTT_Unsubscribe

取消订阅指定topic

```C
int HAL_MQTT_Unsubscribe(void *pClient, char *topicFilter);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pClient| void * | 输入 | MQTT句柄 |
| topicFilter | char * | 输入 | 主题过滤器 |
| ret | int | 返回 | 订阅成功返回packet_id,<br>FAILURE表示失败 |

## IOT_MQTT_IsConnected

确认MQTT是否正处于连接状态

```C
bool IOT_MQTT_IsConnected(void *pClient);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pClient| void * | 输入 | MQTT句柄 |
| ret | bool | 返回 | true表示已连接,<br>false表示已断开 |

## IOT_MQTT_Dynamic_Register 

动态认证连接MQTT服务器

```C 
int IOT_MQTT_Dynamic_Register(MQTTInitParams *pParams); 
```
### 参数列表 

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pParams| MQTTInitParams * | 输入 | MQTT连接参数 |
| ret | bool | 返回 | SUCCESS表示获取成功,<br>FAILURE表示获取失败 |

