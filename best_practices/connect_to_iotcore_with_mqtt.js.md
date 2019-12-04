# 使用mqtt.js接入物联网通信云平台	

对于web即时聊天或者棋类对决等需要实时推送消息给对方的应用，需要建立WEB客户端与服务器的长连接，完成消息的接收与发送。


本实践介绍如何基于WebSocket-MQTT实现应用程序与浏览器的消息上报和下发，详细参考[基于MQTT-WebSocket协议建立连接](/iot/uiot-core/device_develop_guide/deviceconnect/websocketconnect)。

使用WebSocket可以直接下载以下源文件进行测试，示例界面如下：

[代码源文件下载](http://uiot.cn-sh2.ufileos.com/mqtt_over_ws_tool.zip)

![WebSocket在线测试工具](/images/websocket在线测试工具.png)


## 前提条件

1. 参考[创建产品](/iot/uiot-core/console_guide/product_device/create_products\#创建产品)、[创建设备](/iot/uiot-core/console_guide/product_device/create_devcies\#创建设备)，获取产品序列号、设备序列号、设备密钥：
    ```
    ProductSN：ledubff3z85spjmu
    DeviceSN：h9onxtzw0aep7fsr
    DeviceSecret：6g7tjlekwf3sqqqj
    ```

2. 建立连接，web应用先通过设备序列号与用户名进行绑定，然后发放设备密钥，所以web应用一般会以[静态注册](/iot/uiot-core/device_develop_guide/authenticate_devices/unique-certificate-per-device_authentication\#静态注册)的方式建立连接。

   1） 根据静态连接获取到MQTT登录需要的三要素：`ClientID`，`UserName`，`Password`。

MQTT认证参数| 参数值
---|---
ClientID | `ledubff3z85spjmu.h9onxtzw0aep7fsr`<br>规则：`${ProductSN}.${DeviceSN}`
UserName | `ledubff3z85spjmu\|h9onxtzw0aep7fsr\|1`<br>规则：`${ProductSN}\|${DeviceSN}\|${authmode}`<br>`authmode: 1表示静态注册`
Password | `6g7tjlekwf3sqqqj`<br>规则：`${DeviceSecret}`

   2）参考[设备连接](/iot/uiot-core/device_develop_guide/deviceconnect/mqttconnect)，获取MQTT Broker连接域名和TLS CA证书(如使用IE、Edge、Chrome等浏览器CA证书不需要显性加载)：

Broker参数| 参数值
---|---
Broker Address | mqtt-cn-sh2.iot.ucloud.cn （不同区域连接域名不同，参考[已开通区域及域名列表](iot/uiot-core/product_introduction/available_region_url)）
Broker Port | 80或443(使用HTTPS)
KeepAlive | 30秒-1200秒，建议设置为300秒。 **当出现连接出错时，需要仔细检查该参数。**
TLS(CA Certificate file) |[CA证书 下载地址](http://uiot.cn-sh2.ufileos.com/iot_ca.crt) 如使用IE、Edge、Chrome等浏览器不需要下载

   3）按照如下步骤编写代码，接入mqtt broker。

## 代码实现

### CDN 引用

MQTT.js 包可以通过 http://unpkg.com 获得`<script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>`。


### 连接至服务器

```
var host = (d.SSL == "true" ? "wss://" : "ws://") + d.Address + ":" + d.Port 
  
var options = {
  connectTimeout: 30 * 1000, 
  reconnectPeriod: d.Reconnection, 
  clientId: `${d.ProductSN}.${d.DeviceSN}`,
  username: `${d.ProductSN}|${d.DeviceSN}|1`,
  password: d.DeviceSecret,
  clean: true 
} 
client = mqtt.connect(host, options) 
client.on('reconnect', (error) => {
  tip({type:"reconnecting"}) 
})
```

#### 连接地址


上面代码中连接地址为：`(d.SSL == "true" ? "wss://" : "ws://") + d.Address + ":" + d.Port`

即 协议//域名:端口
协议：使用SSL为wss，反之ws；
域名：mqtt-cn-sh2.iot.ucloud.cn （不同区域连接域名不同，参考[已开通区域及域名列表](iot/uiot-core/product_introduction/available_region_url)）
端口：wss为443，ws为80


#### 连接选项

上面代码中， options 是客户端连接选项，以下是主要参数说明，其余参数详见https://www.npmjs.com/package/mqtt#connect。

- keepalive：心跳时间，默认 60秒，设置 0 为禁用；
- clientId： 客户端 ID ，通过 ${ProductSN}.${DeviceSN}生成；
- username：连接用户名，通过 ${ProductSN}|${DeviceSN}|1生成；
- password：连接密码，为设备密码DeviceSecret；
- clean：true，设置为 false 以在离线时接收 QoS 1 和 2 消息；
- reconnectPeriod：默认 1000 毫秒，两次重新连接之间的间隔，客户端 ID 重复、认证失败等客户端会重新连接；
- connectTimeout：默认 30 * 1000毫秒，收到 CONNACK 之前等待的时间，即连接超时时间。

### 订阅/取消订阅

连接成功之后才能订阅，且订阅的主题必须符合 MQTT 订阅主题规则； 通过`client.connected`判断是否连接成功。

```
//订阅消息
client.subscribe(d.Topic, { qos: 0 }, (e, message) => {
  if (message.length != 0 && message[0].qos == 128) {
    tip({type:"sub_fail",topic:d.Topic}); 
  }
  if (message.length != 0 && message[0].qos != 128) {
    tip({type:"sub_success",topic:d.Topic});  
    $('#sub_list').append('<li class=\"list-group-item\">' + d.Topic + '<span class=\"badge\"><span class=\"glyphicon glyphicon-remove\" onclick=\"remove_sub(this)\"></span></span></li>')
  }
});

//取消订阅
client.unsubscribe(btn.parentElement.parentElement.innerText, (e, message) => {
  tip({type:"unsubscribe",text:btn.parentElement.parentElement.innerText});
}
```


### 发布/接收消息

```
//发布消息
client.publish( d.Topic, d.Message, (error) => { 
  tip({type:"publish",topic:d.Topic,message:d.Message});    
})

// 监听接收消息事件
client.on('message', (topic, message) => {
  tip({type:"message",topic:topic,message:message.toString()}) 
})
```

