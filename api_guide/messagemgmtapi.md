# 消息通信

## PublishUIoTCoreMQTTMessage

调用该接口向指定Topic发布消息

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|TopicFullName|string|接收消息的Topic|**Yes**|
|MessageContent|string|要发送的消息主体(base64编码)|**Yes**|
|Qos|int|指定消息的发送方式。取值：0：最多发送一次。1：最少发送一次。如果不传入此参数，则使用默认值0。<br>注：当使用QoS1时，具体服务质量还取决于设备订阅时的QoS，下行和订阅取两者最小值。|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=PublishUIoTCoreMQTTMessage
&Region=cn-sh2
&ProductSN=7ab051kbfhhjakc0
&TopicFullName=/7ab051kbfhhjakc0/h6phdnkjvr90iq6l/hello
&MessageContent=eyJSZXNvdXJjZUlEIjoidWhvc3QtdTN4ZmI1Y28iLCJSZXNvdXJjZU5hbWUiOiJ1YnVudHUtdm5jIiwiUGF0aCI6Ii9oZWxsbyIsIlBvcnQiOjkwOTB9
&Qos=0
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "PublishUIoTCoreMQTTMessageResponse"
}
```



## BroadcastUIoTCoreMQTTMessage

调用该接口向订阅了指定Topic的所有设备发布广播消息。

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|TopicFullName|string|要接收广播消息的Topic全称。|**Yes**|
|MessageContent|string|要发送的消息主体(base64编码)|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=BroadcastUIoTCoreMQTTMessage
&Region=cn-sh2
&ProductSN=7ab051kbfhhjakc0
&TopicFullName=/7ab051kbfhhjakc0/$broadcast/world
&MessageContent=eyJSZXNvdXJjZUlEIjoidWhvc3QtdTN4ZmI1Y28iLCJSZXNvdXJjZU5hbWUiOiJ1YnVudHUtdm5jIiwiUGF0aCI6Ii9oZWxsbyIsIlBvcnQiOjkwOTB9
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BroadcastUIoTCoreMQTTMessageResponse"
}
```
