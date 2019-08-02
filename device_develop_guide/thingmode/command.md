{{indexmenu_n>5}}

# 设备命令
本节介绍关于命令的操作。

## 关于命令的同步异步
UCloud物联网通信云平台同时支持命令的同步和异步，开发者可以根据具体的使用方法灵活决定使用的方式。

同步和异步命令的命令下发流程是一致的，同步调用会保持住HTTP请求，待设备端返回后将返回内容返回给请求者，异步则不关心设备端的返回，直接返回HTTP调用成功请求。

不管同步调用还是异步调用，都需要设备在线，否则云平台会直接返回设备不在线。

### 同步命令
1. 开发者应用服务程序通过[SendUIoTCoreDeviceCommand](../../api_guide/tingmodemgmtapi)下发命令调用接口，`Method`参数设置为`sync-同步`；   
   UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[关于API接入](../../api_guide/api_guidehelp)，其他参数参考[SendUIoTCoreDeviceCommand](../../api_guide/tingmodemgmtapi)。
   ```
   POST  HTTP/1.1
   Host: api.ucloud.cn
   Content-Type: application/json
   Body:
   {
   	"Action": "SendUIoTCoreDeviceCommand",
   	"ProductSN": "70ly1tvowt696r15",
   	"DeviceSN":"00:14:32:e1:72:f1
   ",
    "Identifier": "commandIdentifier",
   	"Input": "eyJpbnB1dDEiOiJpbnB1dFZhbHVlMSJ9", //base64Encode({"input1":"inputValue1"})
   	"Method": "sync",
	"Timeout": 5,
   	"ProjectId": "org-z44lmf12e",
   	"PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
   	"Region": "cn-sh2",
   	"Signature": "dso6b4e35df41b42o3k2e059f6020r7fd51b2pp9u"
   }
   ```
   
2. 调用成功后，云平台保持此HTTP请求，最大5秒超时，并向设备Topic`/$system/${productSN}/${DeviceSN}/tmodel/command`下发一条消息，消息格式为：；
   ```
   {
   	"RequestID": "432542341234",
   	"Identifier": "commandIdentifier",
   	"Input": {
   		"input1": "inputValue1"
   	}
   }
   ```
   参数解释：
   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性；
   - Identifier：调用命令的唯一标识符；
   - Input：输入参数的键值对集合；   

3. 设备端执行相应的命令操作，并在调用API指定的超时时间内进行响应，向Topic `/$system/${productSN}/${DeviceSN}/tmodel/command_reply/${requestid}` 上报一条消息，消息格式为：
   ```
   {
   	"RetCode": 0,
   	"RequestID": "432542341234",
   	"Identifier": "commandIdentifier",
   	"Output": {
   		"output1": "outputValue1"
   	}
   }
   ```
   参数解释：
   - RequestID：返回消息的ID，对应请求消息ID；
   - RetCode：返回码，具体参考[返回码](../../api_guide/retcode)；
   - Identifier：调用命令的唯一标识符；
   - Output：输出参数的键值对集合；云平台将响应作为Response返回给该HTTP请求，否则同步命令失败。

4. 云平台会将设备上报的结果在保持的HTTP请求内返回给开发者应用程序，返回消息为：
   ```
   {
   	"Action": "SendUIoTCoreDeviceCommandResponse",
   	"RetCode": 0,
   	"RequestID": "432542341234",
   	"Output": {
   		"output1": "outputValue1"
   	}
   }
   ```

   如果设备端未能在超时时间内上报结果，云平台会直接给应用程序返回超时消息：
   ```
   {
   	"Action": "SendUIoTCoreDeviceCommandResponse",
   	"RetCode": 100040,
   	"Message":"Command timeout"
   }
   ```
   
   注：应用程序下发的输入参数以及设备端上报的输出参数需要和平台定义的输入和输出Identifier一致，同时取值范围也会做检查，否则会报错，或者为空。

### 异步命令
1. 开发者应用服务程序通过[SendUIoTCoreDeviceCommand](../../api_guide/tingmodemgmtapi)下发命令调用接口，`Method`参数设置为`async-异步`。   
   UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[关于API接入](../../api_guide/api_guidehelp)，其他参数参考[SendUIoTCoreDeviceCommand](../../api_guide/tingmodemgmtapi)。
   ```
   POST  HTTP/1.1
   Host: api.ucloud.cn
   Content-Type: application/json
   Body:
   {
   	"Action": "SendUIoTCoreDeviceCommand",
   	"ProductSN": "70ly1tvowt696r15",
   	"DeviceSN":"00:14:32:e1:72:f1
   ",
    "Identifier": "commandIdentifier",
   	"Input": "eyJpbnB1dDEiOiJpbnB1dFZhbHVlMSJ9", //base64Encode({"input1":"inputValue1"})
   	"Method": "async",
	"Timeout": 5, // 异步调用时，该参数无效
   	"ProjectId": "org-z44lmf12e",
   	"PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
   	"Region": "cn-sh2",
   	"Signature": "dso6b4e35df41b42o3k2e059f6020r7fd51b2pp9u"
   }
   ```
2. 云平台即刻返回HTTP Response。
   ```
   {
   	"Action": "SendUIoTCoreDeviceCommandResponse",
   	"RetCode": 0,
   	"RequestID": "335986033460625408",
   	"Output": {}
   }
   ```
   同时，云平台向设备Topic`/$system/${productSN}/${DeviceSN}/tmodel/command`下发一条消息，消息格式为：；
   ```
   {
   	"RequestID": "335986033460625408",
   	"Identifier": "commandIdentifier",
   	"Input": {
   		"input1": "inputValue1"
   	}
   }
   ```
   参数解释：
   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性；
   - Identifier：调用命令的唯一标识符；
   - Input：输入参数的键值对集合； 
   
3. 设备可以选择即时响应，也可以延后响应，云平台可以将响应通过规则引擎Topic ` /$system/${productSN}/${DeviceSN}/tmodel/command_reply/+`流转到开发者应用服务。
设备端执行相应的命令操作后向Topic `/$system/${productSN}/${DeviceSN}/tmodel/command_reply/${requestid}` 上报一条消息，消息格式为：
   ```
   {
   	"RetCode": 0,
   	"RequestID": "335986033460625408",
   	"Identifier": "commandIdentifier",
   	"Output": {
   		"output1": "outputValue1"
   	}
   }
   ```
   参数解释：
   - RequestID：返回消息的ID，对应请求消息ID；
   - RetCode：返回码，具体参考[返回码]()；
   - Identifier：调用命令的唯一标识符；
   - Output：输出参数的键值对集合；云平台将响应作为Response返回给该HTTP请求，否则同步命令失败。
   
   注：应用程序下发的输入参数以及设备端上报的输出参数需要和平台定义的输入和输出Identifier一致，同时取值范围也会做检查，否则会报错，或者为空。


