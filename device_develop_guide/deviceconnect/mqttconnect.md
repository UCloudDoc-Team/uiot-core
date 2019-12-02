# 基于MQTT-TCP协议建立连接

MQTT协议（Message Queuing Telemetry Transport），叫做遥信消息队列传输。MQTT是一个基于TCP的发布订阅协议，对于有限的内存设备和网络带宽很低的网络不可靠的通信MQTT是比较理想的选择，非常适合物联网通信。



## MQTT连接注意事项
- 支持最高协议版本MQTT3.1，不支持MQTT5.0；
- 不支持will、retain 消息；
- 不支持QoS2；
- 支持clean session；
- 支持基于TCP创建连接；
- 同一注册凭证（`产品序列号`，`设备序列号`，`设备密码`）同时只能有一个设备在线，其它会被踢下线；
- 支持TLSV1.2 版本的协议来建立安全连接，安全级别高；
- MQTT client不能跨Topic订阅或发布消息，只能在自己的所属Topic上订阅或发布消息；



## 具体流程：

MQTT-TCP连接需要先了解[设备注册](/iot/uiot-core/device_develop_guide/authenticate_devices/what_is_authenticate_devices)中提到的静态注册和动态注册，获取 `ClientID`，`UserName`，`Password`。
1. MQTT-TCP如需使用TLS加密传输，需要[下载CA证书](http://uiot.cn-sh2.ufileos.com/ca-cert.pem)；
2. 基于[C-SDK](/iot/uiot-core/device_develop_guide/c_sdk_example/csdkquickstart)进行开发，其他语言可以参考[开源MQTT客户端](https://github.com/mqtt/mqtt.github.io/wiki/libraries?spm=a2c4g.11186623.2.11.793e78dcLHxgZy)进行开发，[MQTT协议](http://mqtt.org/?spm=a2c4g.11186623.2.12.577678dc5E6Qcl)详解可以参考[MQTT官网](http://mqtt.org/?spm=a2c4g.11186623.2.12.577678dc5E6Qcl)；
3. MQTT连接

|参数|详解|
|---|---|
|连接域名 | mqtt-cn-sh2.iot.ucloud.cn （不同区域连接域名不同，参考[已开通区域及域名列表](iot/uiot-core/product_introduction/available_region_url)）|
|端口号 |`1883` 或 `8883(使用TLS)`|
|可变报头（variable header）：Keep Alive  |  Connect指令中需包含Keep Alive（保活时间）。<br>取值范围为30至1200秒。如取值不在此区间，平台拒绝连接。建议取值300秒以上，如网络不稳定，设置高一些。<br>**当出现连接出错时，需要仔细检查该参数。**|
|MQTT的Connect报文参数|参考[静态注册](/iot/uiot-core/device_develop_guide/authenticate_devices/unique-certificate-per-device_authentication)和[动态注册](/iot/uiot-core/device_develop_guide/authenticate_devices/unique-certificate-per-product_authentication)<br>**静态注册为例：**<br>`ClientID：${ProductSN}.${DeviceSN}`<br>`UserName：${ProductSN}\|${DeviceSN}\|${authmode}`<br>`authmode: 静态注册为1；动态注册为2；`<br>`Password：${DeviceSecret}`|


4. 连接成功后需要定期发送心跳包保活，设备端在保活时间间隔内，至少需要发送一次报文（心跳包或数据包），如果物联网平台在该间隔内无法收到任何报文，物联网平台会断开连接，设备端需要进行重连。  



### 消息上行及下行

设备连接成功后即可订阅或发布消息，物联网平台支持
- 自定义Topic，参考[用户自定义Topic](/iot/uiot-core/console_guide/product_device/topic#用户自定义Topic)；
- 基于[设备影子](/iot/uiot-core/console_guide/device_shadow/waht_is_deviceshadow)或者[物模型](/iot/uiot-core/console_guide/thingmode/what_is_thingmode)进行开发，Topic参考[系统Topic](/iot/uiot-core/console_guide/product_device/topic#系统Topic)；
