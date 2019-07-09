{{indexmenu_n>4}}

### 设备影子

设备影子在[云平台操作指南]()中的[设备影子]()中对设备影子已经做了详细的介绍。

在设备端进行开发时，需要使用的仍然`upstream`和`downstream`两个Topic：

Topic | 权限|描述
|---|---|---
|/$system/${ProductSN}/${DeviceSN}/shadow/upstream |发布|更新设备影子
|/$system/${ProductSN}/${DeviceSN}/shadow/downstream | 订阅| 设置期望值

### 设备上报属性值
参考[设备更新设备影子状态]()。

### 设备获取期望值
参考[应用程序更新设备影子期望值]()。
