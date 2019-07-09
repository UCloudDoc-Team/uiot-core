{{indexmenu_n>3}}

### 设备属性
本节介绍设备属性相关的操作。
#### 属性上报
设备端上报属性到云平台。
##### 具体流程
1. 上报属性值  
   设备向Topic `/$system/${productsn}/${devicesn}/tmodel/property/post` 上报一条消息，消息格式为：
   ```
   {
	"RequestID": "100",
	"Property": {
		"propertyIdentifier1": {
			"Value": "propertyValue1",
			"Time": 1524448722000
		},
		"propertyIdentifier2": {
			"Value": "propertyValue2",
			"Time": 1524448722000
		}
	}
   }
   ```
   参数解释：
   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性；
   - Property：所有需要上报的属性集合，包含属性名、属性值、时间戳；
   - Value：属性的值；
   - Time：上报时间戳；
   - Method：上报的方法；
   
2. 云平台响应  
   云平台响应，并向Topic `/$system/${productsn}/${devicesn}/tmodel/property/post_reply` 下发一条消息，消息格式为：
   ```
   {
	  "RequestID": "100",
	  "RetCode": 0,
	  "Message": "success"
   }
   ```
   参数解释：
   - RequestID：返回消息的ID，对应请求消息ID；
   - RetCode：返回码，具体参考[通用返回码]()；
   - Message：返回消息体，成功为"success"，失败则返回具体失败原因；


#### 属性设置
应用服务对设备进行属性设置。
##### 具体流程
1. 设置属性值  
   应用服务通过[云端开发指南-API]()调用接口设置属性，云平台向Topic `/$system/${productsn}/${devicesn}/tmodel/property/set` 下发一条消息，消息格式为：
   ```
   {
   	"RequestID": "100",
   	"Property": {
   		"propertyIdentifier1": "propertyValue1",
   		"propertyIdentifier2": "propertyValue2"
   	}
   }
   ```
   参数解释：
   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性；
   - Property：所有需要设置的属性键值对集合；
   
2. 设备端响应  
   设备端修改属性值，并响应云平台，向Topic `/$system/${productsn}/${devicesn}/tmodel/property/set_reply` 上报一条消息，消息格式为：
   ```
   {
   	"RequestID": "100",
   	"RetCode": 0
   }
   ```
   参数解释：
   - RequestID：返回消息的ID，对应请求消息ID；
   - RetCode：返回码，具体参考[通用返回码]()；

#### 恢复属性
设备掉线后或者属性值丢失后，可以请求云端重新下发属性的最后一次保存的值。

#### 具体流程
1. 请求获取恢复属性文档；  
   设备向Topic `/$system/${productsn}/${devicesn}/tmodel/property/restore`发布一条消息，消息格式为：
   ```
   {
     "RequestID": "100"
   } 
   ```
   参数解释：
   
   - RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性。
   
2. 云平台下发包含最后一次上报的属性值集合；
   云平台向Topic `/$system/${productsn}/${devicesn}/tmodel/property/restore_reply`下发一条消息，消息格式为：
   ```
   {
   	"RetCode": 0,
   	"RequestID": "100",
   	"LatestUpdateTime": 1516541821599,
   	"Property": {
   		"propertyIdentifier1": {
   			"Value": "propertyValue1",
   			"Time": 1516541885630
   		}
   	}
   }
   ```
   参数解释：
   - RetCode：返回码，具体参考[通用返回码]()；
   - RequestID：返回消息的ID，对应请求消息ID；
   - LatestUpdateTime：最近一次属性修改的时间;
   - Property：所有属性集合，包含属性名、属性值、时间戳；
   - Value：属性的值；
   - Time：该属性最后一次上报的时间戳；

#### 全量获取属性
Topic `/$system/${productsn}/${devicesn}/tmodel/property/document`用于获取属性所有值，当属性值发生变化时，会向该Topic发送全量属性。该Topic专用于规则引擎做消息流转，不对设备端开发，即设备端不可以发布和订阅，具体使用参考[规则引擎]()。

