# 消息通信

## PublishUIoTCoreMQTTMessage

调用该接口向指定Topic发布消息

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|ProductSN|string|产品序列号|**Yes**|
|TopicFullName|string|接收消息的Topic|**Yes**|
|MessageContent|string|要发送的消息主体。您需要将消息原文转换成二进制数据，并进行Base64编码，从而生成消息主体。|**Yes**|
|Qos|int|指定消息的发送方式。取值：

0：最多发送一次。

1：最少发送一次。

如果不传入此参数，则使用默认值0。|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=PublishUIoTCoreMQTTMessage
&Region=cn-zj
&ProjectId=YJLaZXEr
&ProductSN=pIrFZjJh
&TopicFullName=mdyxMZGX
&MessageContent=UhejFHmI
&Qos=6
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口]((https://docs.ucloud.cn/api/summary/get_project_list)|No|
|ProductSN|string|产品序列号|**Yes**|
|TopicFullName|string|要接收广播消息的Topic全称。|**Yes**|
|MessageContent|string|要发送的消息主体。您需要将消息原文转换成二进制数据，并进行Base64编码，从而生成消息主体。|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=BroadcastUIoTCoreMQTTMessage
&Region=cn-zj
&ProjectId=EqGcrWQf
&ProductSN=DeTtQAcA
&TopicFullName=GaKFDZBf
&MessageContent=lWPeSdWA
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BroadcastUIoTCoreMQTTMessageResponse"
}
```
