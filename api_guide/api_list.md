# API列表

## 产品管理

|API名称 | 描述|
|---|---|
|[CreateUIoTCoreProduct](uiot-core/api_guide/productmgmtapi#CreateUIoTCoreProduct) | 创建物联网产品|
|[GetUIoTCoreProductInfo](uiot-core/api_guide/productmgmtapi#GetUIoTCoreProductInfo) | 获取产品信息|
|[ModifyUIoTCoreProduct](uiot-core/api_guide/productmgmtapi#ModifyUIoTCoreProduct) | 修改物联网产品|
|[DeleteUIoTCoreProduct](uiot-core/api_guide/productmgmtapi#DeleteUIoTCoreProduct) | 删除物联网产品|
|[GetUIoTCoreProductList](uiot-core/api_guide/productmgmtapi#GetUIoTCoreProductList) | 获取产品信息列表|
|[EnableUIoTCoreDynamicRegister](uiot-core/api_guide/productmgmtapi#EnableUIoTCoreDynamicRegister) | 打开产品下设备动态注册功能|
|[DisableUIoTCoreDynamicRegister](uiot-core/api_guide/productmgmtapi#DisableUIoTCoreDynamicRegister) | 禁用产品下设备动态注册|
|[PublishUIoTCoreProduct](uiot-core/api_guide/productmgmtapi#PublishUIoTCoreProduct) | 发布产品|
|[UnpublishUIoTCoreProduct](uiot-core/api_guide/productmgmtapi#UnpublishUIoTCoreProduct) | 撤销发布产品|



## 设备管理
|API名称 | 描述|
|---|---|
|[CreateUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#CreateUIoTCoreDevice) | 创建物联网设备|
|[ModifyUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#ModifyUIoTCoreDevice) | 修改物联网设备|
|[DeleteUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#DeleteUIoTCoreDevice) | 删除设备|
|[EnableUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#EnableUIoTCoreDevice) | 启用设备|
|[DisableUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#DisableUIoTCoreDevice) | 禁用设备|
|[BatchCreateUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#BatchCreateUIoTCoreDevice) | 批量创建物联网设备|
|[BatchCreateUIoTCoreDeviceWithSN](uiot-core/api_guide/devicemgmtapi#BatchCreateUIoTCoreDeviceWithSN) | 批量创建物联网设备|
|[BatchDeleteUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#BatchDeleteUIoTCoreDevice) | 批量删除设备|
|[BatchEnableUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#BatchEnableUIoTCoreDevice) | 批量启用设备|
|[BatchDisableUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#BatchDisableUIoTCoreDevice) | 批量禁用设备|
|[ResetUIoTCoreDevice](uiot-core/api_guide/devicemgmtapi#ResetUIoTCoreDevice)|重置设备激活状态|
|[GetUIoTCoreDeviceList](uiot-core/api_guide/devicemgmtapi#GetUIoTCoreDeviceList) | 获取单个或批量设备状态、设备详情、设备列表等|
|[GetUIoTCoreInactivatedDevicePasswordFile](uiot-core/api_guide/devicemgmtapi#GetUIoTCoreInactivatedDevicePasswordFile) | 获取未激活设备的密码文件|


## 主题管理

|API名称 | 描述|
|---|---|
|[CreateUIoTCoreProductTopic](uiot-core/api_guide/topicmgmt#CreateUIoTCoreProductTopic) | 创建产品Topic|
|[ModifyUIoTCoreProductTopic](uiot-core/api_guide/topicmgmt#ModifyUIoTCoreProductTopic) | 修改产品Topic|
|[DeleteUIoTCoreProductTopic](uiot-core/api_guide/topicmgmt#DeleteUIoTCoreProductTopic) | 删除产品Topic|
|[GetUIoTCoreProductTopicList](uiot-core/api_guide/topicmgmt#GetUIoTCoreProductTopicList) | 获取产品topic列表|


## 设备影子

|API名称 | 描述|
|---|---|
|[EnableUIoTCoreDeviceShadow](uiot-core/api_guide/deviceshadowmgmtapi#EnableUIoTCoreDeviceShadow) | 打开设备影子|
|[DisableUIoTCoreDeviceShadow](uiot-core/api_guide/deviceshadowmgmtapi#DisableUIoTCoreDeviceShadow) | 关闭设备影子|
|[GetUIoTCoreDeviceShadow](uiot-core/api_guide/deviceshadowmgmtapi#GetUIoTCoreDeviceShadow) | 获取设备影子|
|[UpdateUIoTCoreDeviceShadow](uiot-core/api_guide/deviceshadowmgmtapi#UpdateUIoTCoreDeviceShadow) | 更新设备影子文档|


## 物模型

|API名称 | 描述|
|---|---|
|[GetUIoTCoreDeviceProperty](uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreDeviceProperty) | 获取设备属性|
|[GetUIoTCoreDeviceCommandList](uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreDeviceCommandList) | 获取设备命令列表|
|[GetUIoTCoreDeviceEventList](uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreDeviceEventList) | 获取设备事件列表|
|[SetUIoTCoreDeviceProperty](uiot-core/api_guide/tingmodemgmtapi#SetUIoTCoreDeviceProperty) | 设置设备属性|
|[SendUIoTCoreDeviceCommand](uiot-core/api_guide/tingmodemgmtapi#SendUIoTCoreDeviceCommand) | 发送命令|
|[GetUIoTCoreTModelTemplate](uiot-core/api_guide/tingmodemgmtapi#GetUIoTCoreTModelTemplate) | 获取物模型定义模板|


## 消息通信

|API名称 | 描述|
|---|---|
|[PublishUIoTCoreMQTTMessage](uiot-core/api_guide/messagemgmtapi#PublishUIoTCoreMQTTMessage) | Publish MQTT消息|
|[BroadcastUIoTCoreMQTTMessage](uiot-core/api_guide/messagemgmtapi#BroadcastUIoTCoreMQTTMessage) | 广播消息|

## 规则引擎

|API名称 | 描述|
|---|---|
|[CreateUIoTCoreRule](uiot-core/api_guide/ruleeneinmgmt#CreateUIoTCoreRule) | 创建规则|
|[GetUIoTCoreRuleList](uiot-core/api_guide/ruleeneinmgmt#GetUIoTCoreRuleList) | 获取规则列表|
|[ModifyUIoTCoreRule](uiot-core/api_guide/ruleeneinmgmt#ModifyUIoTCoreRule) | 修改规则|
|[DeleteUIoTCoreRule](uiot-core/api_guide/ruleeneinmgmt#DeleteUIoTCoreRule) | 删除规则|
|[EnableUIoTCoreRule](uiot-core/api_guide/ruleeneinmgmt#EnableUIoTCoreRule) | 启用规则|
|[DisableUIoTCoreRule](uiot-core/api_guide/ruleeneinmgmt#DisableUIoTCoreRule) | 禁用规则|
|[CreateUIoTCoreRuleAction](uiot-core/api_guide/ruleeneinmgmt#CreateUIoTCoreRuleAction) | 创建规则Action|
|[GetUIoTCoreRuleActionList](uiot-core/api_guide/ruleeneinmgmt#GetUIoTCoreRuleActionList) | 获取规则Action列表|
|[ModifyUIoTCoreRuleAction](uiot-core/api_guide/ruleeneinmgmt#ModifyUIoTCoreRuleAction) | 修改规则Action|
|[DeleteUIoTCoreRuleAction](uiot-core/api_guide/ruleeneinmgmt#DeleteUIoTCoreRuleAction) | 删除规则Action|


## 上传文件

|API名称 | 描述|
|---|---|
|[QueryUIoTCoreDeviceFileList](uiot-core/api_guide/uploadfile#QueryUIoTCoreDeviceFileList) | 查询设备上传的文件列表|
|[QueryUIoTCoreDeviceFile](uiot-core/api_guide/uploadfile#QueryUIoTCoreDeviceFile) |获取设备文件信息|
|[GetUIoTCoreDeviceFileURL](uiot-core/api_guide/uploadfile#GetUIoTCoreDeviceFileURL) | 获取设备文件的下载链接|
|[DeleteUIoTCoreDeviceFile](uiot-core/api_guide/uploadfile#DeleteUIoTCoreDeviceFile) | 删除设备文件|

