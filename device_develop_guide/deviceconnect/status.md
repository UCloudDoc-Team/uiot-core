# 获取设备在线状态

云端应用程序有两种方式可以获取到设备的在线状态：

- 实时通知：通过规则引擎转发系统Topic`/$system/${ProductSN}/${DeviceSN}/device/status`到云端应用；
- 静态查询：通过调用接口[GetUIoTCoreDeviceList](/iot/uiot-core/api_guide/devicemgmtapi#getuiotcoredevicelist)获取设备的状态；

注：如果设备通过HTTP上报消息，由于不是长连接，设备状态为未激活或离线状态。

## 实时通知

平台提供在规则引擎系统Topic中配置将设备上线的消息即时流转到用户的业务服务器HTTP、Kafka或者存储到TSDB、MySQL、MongoDB做持久化存储。

#### 具体流程

1. 参考规则引擎[数据流转管理](/iot/uiot-core/console_guide/ruleengine/data_forwarding)，创建消息筛选Topic及筛选字段。


- 设备上线通知消息Payload为：

```json
{
	"ProductSN": "ozuz63kum2i4djb3",
	"DeviceSN": "afnyhnizq9l4l9ev",
	"Status": "Online"
}
```

- 设备下线通知消息Payload为：

```json
{
	"ProductSN": "ozuz63kum2i4djb3",
	"DeviceSN": "afnyhnizq9l4l9ev",
	"Status": "Offline"
}
```

2. 添加执行动作流转到相应的目的地


![转发设备状态](/images/转发设备状态.png)


## 静态查询

参考[关于API接入](/iot/uiot-core/api_guide/api_guidehelp)调用接口GetUIoTCoreDeviceList](/iot/uiot-core/api_guide/devicemgmtapi#getuiotcoredevicelist)可以获取设备状态。



