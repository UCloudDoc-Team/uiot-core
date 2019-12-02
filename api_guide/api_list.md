# API列表

## 产品管理

|API名称 | 描述|
|---|---|
|[CreateUIoTCoreProduct](/iot/uiot-core/api_guide/productmgmtapi#CreateUIoTCoreProduct) | 创建物联网产品|
|[GetUIoTCoreProductInfo](/iot/uiot-core/api_guide/productmgmtapi#GetUIoTCoreProductInfo) | 获取产品信息|
|[ModifyUIoTCoreProduct](/iot/uiot-core/api_guide/productmgmtapi#ModifyUIoTCoreProduct) | 修改物联网产品|
|[DeleteUIoTCoreProduct](/iot/uiot-core/api_guide/productmgmtapi#DeleteUIoTCoreProduct) | 删除物联网产品|
|[GetUIoTCoreProductList](/iot/uiot-core/api_guide/productmgmtapi#GetUIoTCoreProductList) | 获取产品信息列表|
|[EnableUIoTCoreDynamicRegister](/iot/uiot-core/api_guide/productmgmtapi#EnableUIoTCoreDynamicRegister) | 打开产品下设备动态注册功能|
|[DisableUIoTCoreDynamicRegister](/iot/uiot-core/api_guide/productmgmtapi#DisableUIoTCoreDynamicRegister) | 禁用产品下设备动态注册|
|[PublishUIoTCoreProduct](/iot/uiot-core/api_guide/productmgmtapi#PublishUIoTCoreProduct) | 发布产品|
|[UnpublishUIoTCoreProduct](/iot/uiot-core/api_guide/productmgmtapi#UnpublishUIoTCoreProduct) | 撤销发布产品|



## 设备管理
|API名称 | 描述|
|---|---|
|[CreateUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#CreateUIoTCoreDevice) | 创建物联网设备|
|[ModifyUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#ModifyUIoTCoreDevice) | 修改物联网设备|
|[DeleteUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#DeleteUIoTCoreDevice) | 删除设备|
|[EnableUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#EnableUIoTCoreDevice) | 启用设备|
|[DisableUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#DisableUIoTCoreDevice) | 禁用设备|
|[BatchCreateUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#BatchCreateUIoTCoreDevice) | 批量创建物联网设备|
|[BatchCreateUIoTCoreDeviceWithSN](/iot/uiot-core/api_guide/devicemgmtapi#BatchCreateUIoTCoreDeviceWithSN) | 批量创建物联网设备|
|[BatchDeleteUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#BatchDeleteUIoTCoreDevice) | 批量删除设备|
|[BatchEnableUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#BatchEnableUIoTCoreDevice) | 批量启用设备|
|[BatchDisableUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#BatchDisableUIoTCoreDevice) | 批量禁用设备|
|[ResetUIoTCoreDevice](/iot/uiot-core/api_guide/devicemgmtapi#ResetUIoTCoreDevice)|重置设备激活状态|
|[GetUIoTCoreDeviceList](/iot/uiot-core/api_guide/devicemgmtapi#GetUIoTCoreDeviceList) | 获取设备列表|
|[GetUIoTCoreInactivatedDevicePasswordFile](/iot/uiot-core/api_guide/devicemgmtapi#GetUIoTCoreInactivatedDevicePasswordFile) | 获取未激活设备的密码文件|


## 主题管理

|API名称 | 描述|
|---|---|
|[CreateUIoTCoreProductTopic](/iot/uiot-core/api_guide/topicmgmt#CreateUIoTCoreProductTopic) | 创建产品Topic|
|[ModifyUIoTCoreProductTopic](/iot/uiot-core/api_guide/topicmgmt#ModifyUIoTCoreProductTopic) | 修改产品Topic|
|[DeleteUIoTCoreProductTopic](/iot/uiot-core/api_guide/topicmgmt#DeleteUIoTCoreProductTopic) | 删除产品Topic|
|[GetUIoTCoreProductTopicList](/iot/uiot-core/api_guide/topicmgmt#GetUIoTCoreProductTopicList) | 获取产品topic列表|


## 设备影子

|API名称 | 描述|
|---|---|
|[EnableUIoTCoreDeviceShadow](/iot/uiot-core/api_guide/deviceshadowmgmtapi#EnableUIoTCoreDeviceShadow) | 打开设备影子|
|[DisableUIoTCoreDeviceShadow](/iot/uiot-core/api_guide/deviceshadowmgmtapi#DisableUIoTCoreDeviceShadow) | 关闭设备影子|
|[GetUIoTCoreDeviceShadow](/iot/uiot-core/api_guide/deviceshadowmgmtapi#GetUIoTCoreDeviceShadow) | 获取设备影子|
|[UpdateUIoTCoreDeviceShadow](/iot/uiot-core/api_guide/deviceshadowmgmtapi#UpdateUIoTCoreDeviceShadow) | 更新设备影子文档|


## 物模型

|API名称 | 描述|
|---|---|
|[GetUIoTCoreDeviceProperty](/iot/uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreDeviceProperty) | 获取设备属性|
|[GetUIoTCoreDeviceCommandList](/iot/uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreDeviceCommandList) | 获取设备命令列表|
|[GetUIoTCoreDeviceEventList](/iot/uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreDeviceEventList) | 获取设备事件列表|
|[SetUIoTCoreDeviceProperty](/iot/uiot-core/api_guide/tingmodemgmtapi#SetUIoTCoreDeviceProperty) | 设置设备属性|
|[SendUIoTCoreDeviceCommand](/iot/uiot-core/api_guide/tingmodemgmtapi#SendUIoTCoreDeviceCommand) | 发送命令|
|[GetUIoTCoreTModelTemplate](/iot/uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreTModelTemplate) | 获取物模型定义模板|


## 消息通信

|API名称 | 描述|
|---|---|
|[PublishUIoTCoreMQTTMessage](/iot/uiot-core/api_guide/messagemgmtapi#PublishUIoTCoreMQTTMessage) | Publish MQTT消息|
|[BroadcastUIoTCoreMQTTMessage](/iot/uiot-core/api_guide/messagemgmtapi#BroadcastUIoTCoreMQTTMessage) | 广播消息|

## 规则引擎

|API名称 | 描述|
|---|---|
|[CreateUIoTCoreRule](/iot/uiot-core/api_guide/ruleeneinmgmt#CreateUIoTCoreRule) | 创建规则|
|[GetUIoTCoreRuleList](/iot/uiot-core/api_guide/ruleeneinmgmt#GetUIoTCoreRuleList) | 获取规则列表|
|[ModifyUIoTCoreRule](/iot/uiot-core/api_guide/ruleeneinmgmt#ModifyUIoTCoreRule) | 修改规则|
|[DeleteUIoTCoreRule](/iot/uiot-core/api_guide/ruleeneinmgmt#DeleteUIoTCoreRule) | 删除规则|
|[EnableUIoTCoreRule](/iot/uiot-core/api_guide/ruleeneinmgmt#EnableUIoTCoreRule) | 启用规则|
|[DisableUIoTCoreRule](/iot/uiot-core/api_guide/ruleeneinmgmt#DisableUIoTCoreRule) | 禁用规则|
|[CreateUIoTCoreRuleAction](/iot/uiot-core/api_guide/ruleeneinmgmt#CreateUIoTCoreRuleAction) | 创建规则Action|
|[GetUIoTCoreRuleActionList](/iot/uiot-core/api_guide/ruleeneinmgmt#GetUIoTCoreRuleActionList) | 获取规则Action列表|
|[ModifyUIoTCoreRuleAction](/iot/uiot-core/api_guide/ruleeneinmgmt#ModifyUIoTCoreRuleAction) | 修改规则Action|
|[DeleteUIoTCoreRuleAction](/iot/uiot-core/api_guide/ruleeneinmgmt#DeleteUIoTCoreRuleAction) | 删除规则Action|


## 上传文件

|API名称 | 描述|
|---|---|
|[QueryUIoTCoreDeviceFileList](/iot/uiot-core/api_guide/uploadfile#QueryUIoTCoreDeviceFileList) | 查询设备上传的文件列表|
|[QueryUIoTCoreDeviceFile](/iot/uiot-core/api_guide/uploadfile#QueryUIoTCoreDeviceFile) |获取设备文件信息|
|[GetUIoTCoreDeviceFileURL](/iot/uiot-core/api_guide/uploadfile#GetUIoTCoreDeviceFileURL) | 获取设备文件的下载链接|
|[DeleteUIoTCoreDeviceFile](/iot/uiot-core/api_guide/uploadfile#DeleteUIoTCoreDeviceFile) | 删除设备文件|

