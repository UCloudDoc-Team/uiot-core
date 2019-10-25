# API列表

## 产品管理

|API名称 | 描述|
|---|---|
|CreateUIoTCoreProduct | 创建物联网产品|
|GetUIoTCoreProductInfo | 获取产品信息|
|ModifyUIoTCoreProduct | 修改物联网产品|
|DeleteUIoTCoreProduct | 删除物联网产品|
|GetUIoTCoreProductList | 获取产品信息列表|
|EnableUIoTCoreDynamicRegister | 打开产品下设备动态注册功能|
|DisableUIoTCoreDynamicRegister | 禁用产品下设备动态注册|
|PublishUIoTCoreProduct | 发布产品|
|UnpublishUIoTCoreProduct | 撤销发布产品|



## 设备管理
|API名称 | 描述|
|---|---|
|CreateUIoTCoreDevice | 创建物联网设备|
|ModifyUIoTCoreDevice | 修改物联网设备|
|DeleteUIoTCoreDevice | 删除设备|
|EnableUIoTCoreDevice | 启用设备|
|DisableUIoTCoreDevice | 禁用设备|
|BatchCreateUIoTCoreDevice | 批量创建物联网设备|
|BatchCreateUIoTCoreDeviceWithSN | 批量创建物联网设备|
|BatchDeleteUIoTCoreDevice | 批量删除设备|
|BatchEnableUIoTCoreDevice | 批量启用设备|
|BatchDisableUIoTCoreDevice | 批量禁用设备|
|GetUIoTCoreDeviceList | 获取设备列表|
|GetUIoTCoreInactivatedDevicePasswordFile | 获取未激活设备的密码文件|


## 主题管理

|API名称 | 描述|
|---|---|
|CreateUIoTCoreProductTopic | 创建产品Topic|
|ModifyUIoTCoreProductTopic | 修改产品Topic|
|DeleteUIoTCoreProductTopic | 删除产品Topic|
|GetUIoTCoreProductTopicList | 获取产品topic列表|


## 设备影子

|API名称 | 描述|
|---|---|
|EnableUIoTCoreDeviceShadow | 打开设备影子|
|DisableUIoTCoreDeviceShadow | 关闭设备影子|
|GetUIoTCoreDeviceShadow | 获取设备影子|
|UpdateUIoTCoreDeviceShadow | 更新设备影子文档|


## 物模型

|API名称 | 描述|
|---|---|
|GetUIoTCoreDeviceProperty | 获取设备属性|
|GetUIoTCoreDeviceCommandList | 获取设备命令列表|
|GetUIoTCoreDeviceEventList | 获取设备事件列表|
|SetUIoTCoreDeviceProperty | 设置设备属性|
|SendUIoTCoreDeviceCommand | 发送命令|
|GetUIoTCoreTModelTemplate | 获取物模型定义模板|


## 消息通信

|API名称 | 描述|
|---|---|
|PublishUIoTCoreMQTTMessage | Publish MQTT消息|
|BroadcastUIoTCoreMQTTMessage | 广播消息|

## 规则引擎

|API名称 | 描述|
|---|---|
|CreateUIoTCoreRule | 创建规则|
|GetUIoTCoreRuleList | 获取规则列表|
|ModifyUIoTCoreRule | 修改规则|
|DeleteUIoTCoreRule | 删除规则|
|EnableUIoTCoreRule | 启用规则|
|DisableUIoTCoreRule | 禁用规则|
|CreateUIoTCoreRuleAction | 创建规则Action|
|GetUIoTCoreRuleActionList | 获取规则Action列表|
|ModifyUIoTCoreRuleAction | 修改规则Action|
|DeleteUIoTCoreRuleAction | 删除规则Action|



