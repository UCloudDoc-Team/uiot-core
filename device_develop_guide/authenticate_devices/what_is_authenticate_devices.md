# 什么是设备注册

设备注册是指设备第一次接入网络完成设备的激活。设备激活是一个设备根据其唯一的设备凭证（`产品序列号`，`设备序列号`，`设备密码`）完成设备连接到平台的认证过程。

设备注册有两种方式：

- 静态注册（一机一密）：每台设备都有其唯一的凭证（`产品序列号`，`设备序列号`，`设备密码`），静态注册过程参考[静态注册](uiot-core/device_develop_guide/authenticate_devices/unique-certificate-per-device_authentication)；
- 动态注册（一型一密）：设备使用产品的公共凭证（`产品序列号`，`产品密码`）首次连接实现预认证，连接成功后平台对设备上报的设备序列号进行认证，认证通过后下发设备密码给设备，设备再通过设备密码完成注册，具体参考[动态注册](uiot-core/device_develop_guide/authenticate_devices/unique-certificate-per-product_authentication);
