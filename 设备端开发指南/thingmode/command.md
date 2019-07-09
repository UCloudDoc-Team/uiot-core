{{indexmenu_n>5}}

### 设备命令
本节介绍关于命令的操作，设备端对于命令的同步异步是不敏感的。

#### 关于命令的同步异步
UCloud物联网通信云平台同时支持命令的同步和异步，开发者可以根据具体的使用方法灵活决定使用的方式。
##### 同步命令（此处应该有图）
1. 开发者应用服务程序通过[云端开发命令调用API]()下发命令调用接口，参数设置为同步；
2. 云平台保持此HTTP请求，并向设备Topic`/$system/${productsn}/${devicesn}/tmodel/command`下发命令；
3. 设备须在调用API指定的时间内进行响应，云平台将响应作为Response返回给该HTTP请求，否则同步命令失败。

##### 异步命令（此处应该有图）
1. 开发者应用服务程序通过[云端开发命令调用API]()下发命令调用接口，参数设置为异步，云平台即刻返回HTTP Response；
2. 云平台向设备Topic`/$system/${productsn}/${devicesn}/tmodel/command`下发命令；
3. 设备可以选择即时响应，也可以延后响应，云平台将响应通过规则引擎流转到开发者应用服务。

#### 命令下发
应用服务对设备进行命令下发，设备执行相应的动作。
##### 具体流程
1. 命令下发  
   应用服务通过[云端开发指南-API]()调用接口同步或异步下发命令，云平台向Topic `/$system/${productsn}/${devicesn}/tmodel/command` 下发一条消息，消息格式为：
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
   
2. 设备端响应  
   设备端执行相应的命令操作，并响应云平台，向Topic `/$system/${productsn}/${devicesn}/tmodel/command_reply/${requestid}` 上报一条消息，消息格式为：
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
   - RetCode：返回码，具体参考[通用返回码]()；
   - Identifier：调用命令的唯一标识符；
   - Output：输出参数的键值对集合；