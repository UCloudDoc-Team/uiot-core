# 设备期望属性
设备期望属性，是指对设备进行属性设置时如果设备不在线，云平台将缓存需要设置的值，待设备上线后再来获取期望属性；设备在线时执行正常的属性设置流程。

## 具体流程
1. 设备不在线时，开发者应用程序通过[SetUIoTCoreDeviceProperty](uiot-core/api_guide/tingmodemgmtapi#SetUIoTCoreDeviceProperty)下发命令调用接口，`Desired`参数设置为`true`，云平台缓存设置值；   
   UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[关于API接入](uiot-core/api_guide/api_guidehelp)，其他参数参考[SetUIoTCoreDeviceProperty](uiot-core/api_guide/tingmodemgmtapi#SetUIoTCoreDeviceProperty)。
   ```
   POST  HTTP/1.1
   Host: api-cn-sh2.iot.ucloud.cn
   Content-Type: application/json
   Body:
   {
   	"Action": "SetUIoTCoreDeviceProperty",
   	"ProductSN": "70ly1tvowt696r15",
   	"DeviceSN":"00:14:32:e1:72:f1
   ",
   	"Property": "eyJwcm9wZXJ0eUlkZW50aWZpZXIxIjoiZGVzaXJlZFByb3BlcnR5VmFsdWUxIn0=", //base64Encode({"propertyIdentifier1":"desiredPropertyValue1"})
   	"Desired": true,
   	"ProjectId": "org-z44lmf12e",
   	"PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
   	"Region": "cn-sh2",
   	"Signature": "lue6b4e35df9e872232po59f6020r7fd51b28e56"
   }
   ```
2. 设备在线时，会作为一条【设置属性】消息通过`/$system/${productSN}/${DeviceSN}/tmodel/property/set`下发给设备端，如果设备不在线，上线后可以请求获取期望属性值；  
   设备上线后向Topic `/$system/${productSN}/${DeviceSN}/tmodel/property/desired/get`发布一条消息，消息格式为：
   ```
   {
   	"RequestID": "100",
   	"Require": [
   		"propertyName1",
   		"propertyName2"
   	]
   }
   ```
   参数解释：
   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性；
   - Require：需要获取的期望属性的标识符的集合；
   
2. 下发期望属性值；
   云平台向Topic `/$system/${productSN}/${DeviceSN}/tmodel/property/desired/get_reply`下发一条消息，消息格式为：
   ```
   {
   	"RetCode": 0,
   	"RequestID": "100",
   	"Desired": {
   		"propertyIdentifier1": {
   			"Value": "desiredPropertyValue1",
   			"Version": 1
   		}
   	}
   }
   ```
   参数解释：
   - RetCode：返回码，具体参考[返回码](uiot-core/api_guide/retcode)；
   - RequestID：返回消息的ID，对应请求消息ID；
   - Desired：返回的期望属性的集合;
   - Value：指定属性标识符的值；
   - Version：当前期望的version值，当删除期望值时该Version值需要一致。开发者应用程序每调用一次Version版本号加一次；
 
3. 请求删除期望属性值
   设备更新属性成功后，向Topic `/$system/${productSN}/${DeviceSN}/tmodel/property/desired/delete`发布一条消息，消息格式为：
   ```
   {
   	"RequestID": "100",
   	"Delete": {
   		"propertyIdentifier1": {
   			"Version": 1
   		}
   	}
   }
   ```
   参数解释：
   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性；
   - Delete：需要删除的期望属性的标识符的集合；
   - propertyIdentifier1：需要删除的期望属性的标识符；
   - Version：Version需要和当前云端的缓存Version一致，否则删除不生效，需要重新通过Topic `/$system/${productSN}/${DeviceSN}/tmodel/property/desired/get`获取最新的期望值更新，再删除。

4. 响应删除成功
   云平台向Topic `/$system/${productSN}/${DeviceSN}/tmodel/property/desired/delete_reply`下发一条消息，消息格式为：
   ```
   {
   	"RequestID": "100",
   	"RetCode": 0,
   	"Message": "success"
   }
   ```
   参数解释：
   - RetCode：返回码，具体参考[返回码](uiot-core/api_guide/retcode)；
   - RequestID：返回消息的ID，对应请求消息ID；
   - Message：返回消息体，成功为"success"，失败则返回具体失败原因。