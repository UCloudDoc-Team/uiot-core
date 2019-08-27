{{indexmenu_n>3}}

# 基于HTTP协议建立连接

HTTP(Hypertext Transfer Protocol )协议接入是指通过HTTP的方式将设备接入到UCloud IoT-Core通信云平台，将数据上传到云端。

由于HTTP的采用请求/响应的模型，所以HTTP仅能用于数据上报，不能用于命令的下发。



## HTTP连接注意事项

- 使用HTTPS协议，支持TLS V1.2版本；

- CA证书为国际授信的域名证书，也可以直接下载[CA证书](http://uiot.cn-sh2.ufileos.com/iot_ca.crt)；

- HTTP请求只支持POST方式；

- 基于MQTT的Topic规范，数据上报到MQTT的某个Topic；

- 上报数据请求URL：**https://http-cn-sh2.iot.ucloud.cn/topic/${topic}**。其中**${topic}**的值是指具备发布权限的[Topic](../../console_guide/product_device/topic)。不支持以 ?query_String=xxx 格式传参；

- HTTP协议只能用于[静态注册](../device_develop_guide/authenticate_devices/unique-certificate-per-device_authentication)的设备上行数据，不支持[动态注册](../device_develop_guide/authenticate_devices/unique-certificate-per-product_authentication)的情况；

- HTTP可以和MQTT同时使用，但要做好数据的同步；

- 数据上行传输的数据大小限制为 128 KB；

- 设备静态注册请求的HTTP header中的**Content-Type**必须为 **application/json**；

- 数据上报请求的HTTP header中的**Content-Type**必须为 **application/octet-stream**；

- 设备注册成功后，HTTP服务会返回Token，有效期为7天，需要做好Token续期服务；


## 具体流程：


1\. 获取到设备的注册凭证：**产品序列号**，**设备序列号**，**设备密码**，分别表示为**${ProductSN}**，**${DeviceSN}**，**${DevSecret}** 

2\. 下载TLS证书，[下载根证书](http://uiot.cn-sh2.ufileos.com/iot_ca.crt)；

3\. 设备注册。通过HTTP POST请求获取上报数据的Token，见**返回参数**：

```
POST /auth HTTP/1.1
Host: http-cn-sh2.iot.ucloud.cn
Content-Type: application/json
Authorization: 47b0194e52ed1d1630830b66709b906a1e201ba410101cfaf9381bbde53a0d85
body: {"ProductSN":"ZG1EvTEa7NN","DeviceSN":"NlwaSPXsCpTQuh8FxBGH","Timestamp":"1501668289957"}
``` 


**参数说明**

|参数|说明|
|---|---|
|Method|请求方法。只支持 POST 方法。|
|URL|**/auth**，URL 地址|
|Host|HTTP服务地址|
|Content-Type|body 数据的编码格式。目前只支持 **application/json**|
|Authorization|使用设备密码签名。签名计算格式为 **HMAC-SHA256(DeviceSecret, body)**|
|body|设备认证信息。JSON 数据格式。具体信息，请参见下表 body 参数。|


**body 参数**


|参数名称|必选|类型|描述|
|---|---|---|---|
|ProductSN|是|string|产品序列号|
|DeviceSN|是|string|设备序列号|
|Timestamp|否|int64|时间戳（如填写时间误差不超过 3600 秒）|


**返回参数**

```
{
  "RetCode": 0,
  "Message": "Success",
  "Token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJEZXZpY2VTTiI6InRlc3QxIiwiUHJvZHVjdFNOIjoiZzR3ZmFycTMweXp4YXkyMyIsImV4cCI6MTU2NzA1ODg5OSwiaWF0IjoxNTY2NDU0MDk5fQ.wN1XNVciI27nTeIqCjbYKdmTaifJrGJm_DmDDpIoabs"
}
```

**错误码**

|RetCode|Message|备注|
|---|---|---|
|130|Service is temporarily unavailable, we are working hard to restore it, please retry later|服务暂时不可用。|
|171|Signature error|签名错误。|
|230|Parameter error, please reenter|请求的参数异常。|
|100070|Timestamp error|时间戳错误，误差超过限制。|
|100071|Product or device not exist|产品或设备不存在。|
|100072|Device disabled|设备已禁用。|


4\. 上报数据。将数据发送数据到某个 Topic。  

HTTP平台支持发布权限的自定义或系统Topic。

- 自定义Topic，参考[用户自定义Topic](../console_guide/product_device/topic#用户自定义Topic)；

- [系统Topic](../console_guide/product_device/topic#系统Topic)，参考[设备影子](../console_guide/device_shadow/waht_is_deviceshadow)或者[物模型](../console_guide/thingmode/what_is_thingmode)Topic；


```
POST /topic/${topic} HTTP/1.1
Host: http-cn-sh2.iot.ucloud.cn
Password: ${token}
Content-Type: application/octet-stream
body: ${your_data}
```


**参数说明**


|参数|说明|
|---|---|
|Method|请求方法。只支持 POST 方法。|
|URL|`/topic/${topic}`。其中，变量 ${topic} 需替换为数据发往的目标Topic。|
|Host|endpoint 地址|
|Content-Type|body 数据的编码格式。目前只支持 application/octet-stream|
|Password|放在Header中的参数，取值为调用设备认证接口 auth 返回的 token 值。|
|body|发往 ${topic} 的数据内容，长度不超过 128 KB。|


**返回参数**


```
{
  "RetCode": 0,
  "Message": "Success",
  "MessageID": "349022219378098176"
}
```

**错误码**


|RetCode|Message|备注|
|---|---|---|
|130|Service is temporarily unavailable, we are working hard to restore it, please retry later|服务暂时不可用。|
|230|Parameter error, please reenter|请求的参数异常。|
|100071|Product or device not exist|产品或设备不存在。|
|100072|Device disabled|设备已禁用。|
|100073|Check token error|token错误。需重新调用auth进行鉴权，获取token。|
|100074|Token is expired|token过期。需重新调用auth进行鉴权，获取token。|
|100075|ACL Failed|ACL 失败，无相应 topic 权限。|
|100076|Maximum request length exceeded|body 长度超过限制。|
|100077|Publish message Failed|数据发送失败。|

