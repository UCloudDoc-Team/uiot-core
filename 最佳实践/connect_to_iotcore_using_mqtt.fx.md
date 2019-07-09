{{indexmenu_n>1}}


###使用MQTT.fx接入物联网通信云平台	

本实践介绍一个完整的利用物联网云平台（UIoT-Core）实现应用程序与设备的消息上报和命令下发。

实践基于模拟客户端MQTT.fx，该软件免费使用，可以在其[官方网站下载](http://mqttfx.jensd.de/index.php/download)。

本文列举了通过设备影子和自定义Topic实现上行、下行的通信。用户也可以按照该实践完成通过物模型的上行、下行通信。


#### 前提条件
1. 参考[创建产品]()、[创建设备]()，获取产品序列号、设备序列号、设备密钥：
```
ProductSN：qn4hvcjiyqt2069t
DeviceSN：4ythk4cav6ph4310
DeviceSecret：6g7tjlekwf3sqqqj
```

2. 建立连接，本例以[静态注册]()的方式建立连接，如需动态注册请参考[动态注册]()。  

   1） 根据静态连接获取到MQTT登录需要的三要素：`ClientID`，`UserName`，`Password`。

    MQTT认证参数| 参数值
    ---|---
    ClientID | qn4hvcjiyqt2069t.4ythk4cav6ph4310<br>`规则：${ProdID}.${DevSN}`
    UserName | qn4hvcjiyqt2069t\|4ythk4cav6ph4310\|1<br>`规则：${ProdID}\|${DevSN}\|${authmode}`<br>`authmode: 1表示静态注册；2表示动态注册`
    Password | 6g7tjlekwf3sqqqj<br>`规则：${DevSecret}`
   
   2）参考[设备连接]()，获取MQTT Broker连接域名和TLS CA证书：
    Broker参数| 参数值
    ---|---
    Broker Address | ==cn-sh2.iot.ucloud.cn==
    Broker Port | 1883
    TLS(CA Certificate file) |[root.cer 下载地址]()
   
   3）打开MQTT.fx软件，连接成功
    按照下图的顺序依次输入相应的参数值。
    - 输入Broker Address、Broker Port
    - 输入User Name、 Passwo
    - 输入TLS证书
    - 点击<Apply>，提交配置
    - 点击<Connect>，进行连接
    <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/B02C57C3E0984246B0926DE7FC95009A/31732" width="900" />
    输入TLS证书：
    <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />
   
#### 通过设备影子

设备影子的具体详情参考[设备影子]()，本例中设备影子的Topic为：

Topic | 权限|描述
|---|---|---
|/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/upstream |发布|更新设备影子
|/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/downstream | 订阅| 设置期望值

##### 上行测试（发送设备属性）
1. 在MQTT.fx操作界面，点击<Publish>，输入Topic：`/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/upstream`；
2. 根据[设备影子]()文档输入Payload，上报属性`"color" : "red"`；
   ```
   { 
    "Method" : "update" , 
    "State" : { 
        "Reported" : { 
            "color" : "red" 
        } 
    }, 
    "Version" : 0 
   }
   ```
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />
3. 在控制台查看设备影子的更新，上行数据上报成功，如图：
  
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />

4. 也可以在日志里面查看上报成功结果，如图：

   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />


##### 下行测试（设置期望值）
1. 在MQTT.fx操作界面，点击<Subscribe>，输入Topic：`/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/downstream`；
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />

2. 下发期望值，有两种方法：  
   ① 参考[设备影子]()，<编辑>设备影子，输入<Desired>值：
   ```
   {
    "color":"green"
   }
   ```
   ② 使用云端API进行调用，参考[UpdateUIoTCoreDeviceShadow]()，或直接通过[API测试界面](https://console.ucloud.cn/uapi/ucloudapi)测试。
   
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />
3. 在MQTT.fx操作界面看到下发消息；
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />



#### 通过自定义Topic
自定义Topic的具体详情参考[用户自定义Topic]()，创建上行和下行两个自定义Topic为：

Topic | 权限|描述
|---|---|---
|/qn4hvcjiyqt2069t/4ythk4cav6ph4310/uplink |发布|上行消息
|/qn4hvcjiyqt2069t/4ythk4cav6ph4310/downlink | 订阅| 下行消息
##### 上行测试
1. 在MQTT.fx操作界面，点击<Publish>，输入Topic：`/qn4hvcjiyqt2069t/4ythk4cav6ph4310/uplink`；
2. 输入任意内容的Payload：
   ```
   {
     "payload":"test"
   }
   ```

2. 在日志里面查看上报成功结果，如图：

   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />
   
3. 也可以通过规则引擎M2M、HTTP、MQ等进行消息的接收消费。


##### 下行测试
1. 在MQTT.fx操作界面，点击<Subscribe>，输入Topic：`/qn4hvcjiyqt2069t/4ythk4cav6ph4310/downlink`；
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />

2. 使用云端API进行调用，参考[PublishUIoTCoreMQTTMessage]()，或直接通过[API测试界面](https://console.ucloud.cn/uapi/ucloudapi)测试。
  
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />
3. 在MQTT.fx操作界面看到下发消息；
   <img src="https://note.youdao.com/yws/public/resource/933aa0c3d8a8aaef05ec16f9dbe3d963/xmlnote/39855BEFD7124E54811CC6E67A5FB445/31763" width="900" />
