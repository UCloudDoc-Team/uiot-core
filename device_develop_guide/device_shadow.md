# 设备影子

设备影子在控制台操作指南中已经做了详细介绍。详细参考[设备影子](../console_guide/device_shadow/waht_is_deviceshadow)。

在设备端进行开发时，涉及的Topic：

|Topic| 权限|描述|
|---|---|---|
|/$system/${ProductSN}/${DeviceSN}/device/status|订阅|设备状态|
|/$system/${ProductSN}/${DeviceSN}/shadow/upstream |发布|上行操作设备影子（更新、删除）|
|/$system/${ProductSN}/${DeviceSN}/shadow/downstream | 订阅| 设置期望值|
|/$system/${ProductSN}/${DeviceSN}/shadow/get|发布|获取设备影子|
|/$system/${ProductSN}/${DeviceSN}/shadow/get_reply|订阅|获取设备影子返回|
|/$system/${ProductSN}/${DeviceSN}/shadow/document|-|设备影子发生变化时将发送完整的设备影子文档(仅用于规则引擎)|



## 设备端设备影子支持的功能

对设备影子的操作包括，具体参考[设备影子相关操作](../console_guide/device_shadow/operation_guide)：
- 设备端获取设备影子文档；
- 设备端上报状态更新设备影子；
- 设备端删除设备影子属性；
- 设备端重置设备影子版本；

