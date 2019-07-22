{{indexmenu_n>3}}

# 设备连接

# 基于MQTT协议建立连接
MQTT协议（Message Queuing Telemetry Transport），叫做遥信消息队列传输。MQTT是一个基于TCP的发布订阅协议，对于有限的内存设备和网络带宽很低的网络不可靠的通信MQTT是比较理想的选择，非常适合物联网通信。

## MQTT连接注意事项（需要修改添加，session是否支持，如果支持消息保存时长）
- 支持最高协议版本MQTT3.1，不支持MQTT5.0；
- 不支持will、retain 消息；
- 不支持QoS2；
- 支持基于TCP创建连接；
- 同一注册凭证（`产品序列号`，`设备序列号`，`设备密码`）同时只能有一个设备在线，其它会被踢下线；
- 支持 TLSV1, TLSV1.1，TLSV1.2 版本的协议来建立安全连接，安全级别高；
- MQTT client不能跨Topic订阅或发布消息，只能在自己的所属Topic上订阅或发布消息；

## 具体流程：
MQTT连接需要先了解[设备注册]()中提到的静态注册和动态注册，获取 `ClientID`，`UserName`，`Password`。
1. MQTT必须是用TLS加密传输，需要[下载根证书]()；
2. 基于[C-SDK]()进行开发，其他语言可以参考[开源MQTT客户端](https://github.com/mqtt/mqtt.github.io/wiki/libraries?spm=a2c4g.11186623.2.11.793e78dcLHxgZy)进行开发，[MQTT协议](http://mqtt.org/?spm=a2c4g.11186623.2.12.577678dc5E6Qcl)详解可以参考[MQTT官网](http://mqtt.org/?spm=a2c4g.11186623.2.12.577678dc5E6Qcl)；
3. MQTT连接

|参数| 详解|
|---|---|
|连接域名 | 域名的介绍|
|可变报头（variable header）：Keep Alive | Connect指令中需包含Keep Alive（保活时间）。保活心跳时间取值范围为30至1200秒。如果心跳时间不在此区间内，物联网平台会拒绝连接。建议取值300秒以上。如果网络不稳定，将心跳时间设置高一些。
MQTT的Connect报文参数|参考[静态注册]()和[动态注册]()<br>**静态注册为例：**<br>```ClientID：${ProductSN}.${DeviceSN}```<br>```UserName：${ProductSN}|${DeviceSN}|${authmode}```<br>```authmode: 静态注册为1；动态注册为2```<br>``` Password：${DevSecret}```|  
4. 连接成功后需要定期发送心跳包保活，设备端在保活时间间隔内，至少需要发送一次报文，包括ping请求到物联网平台，如果物联网平台在该间隔内无法收到任何报文，物联网平台会断开连接，设备端需要进行重连。  
连接保活时间的取值范围为30至1200秒。建议取值300秒以上。


## 消息上行及下行
设备连接成功后即可订阅或发布消息，物联网平台支持
- 自定义Topic，参考[用户自定义Topic]()；
- 基于[设备影子]()或者[物模型]()进行开发，Topic参考[系统Topic]()；