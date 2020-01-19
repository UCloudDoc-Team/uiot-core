# 上传文件


上传文件是指设备端通过HTTP通道上传较大文件，因为MQTT对消息大小有一定的限制，上传文件可能是视频截取文件、历史消息数据、离线数据等。


## 上传文件注意事项

- 必须使用HTTPS协议，支持TLS V1.2版本；
- CA证书为国际授信的域名证书，也可以直接下载[CA证书](http://uiot.cn-sh2.ufileos.com/iot_ca.crt)；



## 具体流程

设备上传文件的流程如下所示：

1. 获取上传文件目标URL；

	设备端HTTPS请求获取上传文件的目标URL以及上传文件的Authorization

```
POST /api/v1/url HTTP/1.1
Host: file-cn-sh2.iot.ucloud.cn
Content-Type: application/json
Authorization: 325fb7b81989204aa75b02212d98e2d377e7140c010b7ad0a6e17fb6aea06543
body: {"ProductSN":"ZG1EvTEa7NN","DeviceSN":"NlwaSPXsCpTQuh8FxBGH","FileName":"file1.txt","FileSize":102654,"MD5":"5bd57f342dd954e3c1cebac6c6660a79","Content-Type":"plain/text"}
```

**参数说明**

|参数|说明|
|---|---|
|Method|请求方法。只支持 POST 方法。|
|URL|`/api/v1/url`，URL 地址|
|Host|`file-cn-sh2.iot.ucloud.cn`，端口必须为443。（不同区域连接域名不同，参考[已开通区域及域名列表](iot/uiot-core/product_introduction/available_region_url)）|
|Content-Type|body 数据的编码格式。目前只支持 application/json|
|Authorization|使用设备密码签名。签名计算格式为 `HMAC-SHA256(DeviceSecret, body)`|
|body|设备认证信息。JSON 数据格式。具体信息，请参见下表 body 参数。|

**body参数**

|参数名称|必选|类型|描述|
|---|---|---|---|
|ProductSN|是|string|产品序列号|
|DeviceSN|是|string|设备序列号|
|FileName|是|string|文件名称|
|FileSize|是|int|文件大小|
|MD5|是|string|文件的MD5|
|Content-Type|是|string|文件数据的编码格式，比如plain/text，application/zip等|

**返回**

```
{
	"RetCode": 0,
	"URL": "https://uiotcore-55977351-55738012.cn-sh2.ufileos.com/ProductSN/DeviceSN/fileName",
	"Authorization": "Ucloud eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJEZXZpY2VTTiI6InRlc3QxIiwiUHJvZHVjdFNOIjoiZzR3ZmFycTMweXp4YXkyMyIsImV4cCI6MTU2NzA1ODg5OSwiaWF0IjoxNTY2NDU0MDk5fQ.wN1XNVciI27nTeIqCjbYKdmTaifJrGJm_DmDDpIoabs"
}
```


2. 设备根据返回的URL和Authorization上传文件；

```
PUT  HTTP/1.1
```

**参数说明**

|参数|说明|
|---|---|
|Method|请求方法。只支持 PUT 方法。|
|URL|`url`，请求上传文件返回的 URL 地址|

**Header参数**

|参数|说明|必填项|
|---|---|---|
|Authorization|请求上传文件返回的Authorization |必填|
|Content-Type|文件数据的编码格式，比如plain/text，application/zip等|必填|
|Content-MD5|文件数据的MD5|必填|

**Body参数**

|参数|说明|必填项|
|---|---|---|
|Body|上传文件的数据 | 必填 |

**返回参数**

```
- status为200时返回空json
- 其他返回
{
	"RetCode": xxx,
	"ErrMsg": "xxxxxxxx"
}
```

其中RetCode参考[UFile 错误码列表](https://docs.ucloud.cn/api/ufile-api/error_code)。

