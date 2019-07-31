{{indexmenu_n>4}}

# 设备事件

本节介绍设备事件相关的操作。

## 设备上报事件

设备端上报事件到云平台，时间上报不支持多个同时上报。

### 具体流程

1. 上报事件内容  

   设备向Topic **/$system/${productSN}/${DeviceSN}/tmodel/event/post** 上报一条消息，消息格式为：

```
{
	"RequestID": "100",
	"Identifier": "eventIdentifier",
	"Output": {
		"output1": "outputValue1"
	},
	"Time": 1524448723000
}
```

   参数解释：

   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性；
   - Identifier：事件的标识符；
   - Output：事件输出参数键值对的集合；
   - Time：上报时间戳；
   - Method：上报的方法；

2. 云平台响应  

   上报成功后，云平台响应，并向Topic **/$system/${productSN}/${DeviceSN}/tmodel/event/post_reply** 下发一条消息，消息格式为：

```
{
  "RequestID": "100",
  "RetCode": 0,
  "Message": "success"
}
```

   参数解释：

   - RequestID：返回消息的ID，对应请求消息ID；
   - RetCode：返回码，具体参考[通用返回码](../api_guide/retcode)；
   - Message：返回消息体，成功为"success"，失败则返回具体失败原因；
