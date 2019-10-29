# 设备端开发概述

## 基于开源MQTT客户端开发

UCloud物联网通信云平台基于标准的MQTT协议提供消息收发能力，用户可以根据选择[开源MQTT客户端](https://github.com/mqtt/mqtt.github.io/wiki/libraries?spm=a2c4g.11186623.2.11.793e78dcLHxgZy)进行移植，从而实现与物联网平台的设备认证、消息收发、设备管理、日志管理等功能。


注：基于开源的MQTT客户端开发，则不能使用平台提供的设备影子、物模型、OTA固件升级、文件上传等高级功能。


## 基于SDK开发

### 设备端开发语言选择

开发语言 | 支持功能 
---|---
C | 参考例子：[设备注册](../device_develop_guide/c_sdk_example/mqttinterface#设备身份认证) [设备连接](../device_develop_guide/c_sdk_example/mqttinterface#设备身份认证) [设备影子](../device_develop_guide/c_sdk_example/deviceshadowinterface) [物模型](../device_develop_guide/c_sdk_example/thingmodelinterface) [设备OTA升级](../device_develop_guide/c_sdk_example/otainterface)
其他语言| [设备注册](../device_develop_guide/authenticate_devices/what_is_authenticate_devices) [设备连接](../device_develop_guide/connecting_devices) 参考[开源MQTT客户端](https://github.com/mqtt/mqtt.github.io/wiki/libraries?spm=a2c4g.11186623.2.11.793e78dcLHxgZy)开发 <br>高级功能需要参考本章节的相关介绍。<br>[设备影子](../device_develop_guide/device_shadow) <br>[物模型](../device_develop_guide/thingmode/what_is_thingmode) <br>[设备OTA升级](../device_develop_guide/ota)<br>[文件上传](../device_develop_guide/uploadfile) 


操作步骤：
1. [注册](https://passport.ucloud.cn/#register)UCloud云服务，如已注册请直接第2步。
2. 登录进入UCloud[物联网平台](https://console.ucloud.cn/uiot)。
3. 根据云平台操作指南在控制台进行相关的操作，比如创建产品，创建设备，创建Topic，创建规则引擎等。
4. 基于C-SDK或其他语言进行设备端开发。
