{{indexmenu_n>1}}

# 物模型定义
物模型在[控制台操作指南](../../console_guide/thingmode/thingmode_guide)已经做了详细名词解释，物模型从属性、命令、事件三个维度对设备进行抽象。
本章将会详细介绍设备端基于物模型的开发，以及设备端、物联网通信云平台、应用服务之间的交互流程，分别参考[获取物模型定义JSON文档](get_json)，[设备属性](property)，[设备事件](event)，[设备命令](command)，[设备期望属性](desired)。
## 物模型涉及的所有Topic

|Topic | 权限|描述|
|---|---|---|
|/$system/${ProductSN}/${DeviceSN}/tmodel/template/get|发布|请求获取物模型功能定义JSON描述|
|/$system/${ProductSN}/${DeviceSN}/tmodel/template/get_reply | 订阅| 返回物模型功能定义JSON描述|
|/$system/${productSN}/${DeviceSN}/tmodel/property/post|发布|上报属性|
|/$system/${productSN}/${DeviceSN}/tmodel/property/post_reply|订阅|云平台对设备属性的响应|
|/$system/${productSN}/${DeviceSN}/tmodel/property/set|订阅|云平台设置属性|
|/$system/${productSN}/${DeviceSN}/tmodel/property/set_reply|发布|设备端对设置属性的响应|
|/$system/${productSN}/${DeviceSN}/tmodel/property/restore|发布|请求恢复属性|
|/$system/${productSN}/${DeviceSN}/tmodel/property/restore_reply|订阅|云平台返回需要恢复的属性值|
|/$system/${productSN}/${DeviceSN}/tmodel/property/desired/get|发布|获取期望属性|
|/$system/${productSN}/${DeviceSN}/tmodel/property/desired/get_reply|订阅|云平台返回期望属性|
|/$system/${productSN}/${DeviceSN}/tmodel/property/desired/delete|发布|删除期望属性|
|/$system/${productSN}/${DeviceSN}/tmodel/property/desired/delete_reply|订阅|云平台返回删除结果|
|/$system/${productSN}/${DeviceSN}/tmodel/property/document|-|设备的物模型属性发生变化时将发送完整的物模型属性文档(仅用于规则引擎)|
|/$system/${productSN}/${DeviceSN}/tmodel/event/post|发布|上报事件|
|/$system/${productSN}/${DeviceSN}/tmodel/event/post_reply|订阅|云平台对上报事件的响应|
|/$system/${productSN}/${DeviceSN}/tmodel/command|订阅|云平台下发命令|
|/$system/${productSN}/${DeviceSN}/tmodel/command_reply/${requestid}|发布|设备端对云平台下发命令的响应|