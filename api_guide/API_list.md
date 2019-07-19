{{indexmenu_n>2}}

# API列表

## 产品管理

API名称 | 描述
---|---
CreateUIoTCoreProduct | 创建物联网产品
GetUIoTCoreProductInfo | 获取产品信息
ModifyUIoTCoreProduct | 修改物联网产品
DeleteUIoTCoreProduct | 删除物联网产品
GetUIoTCoreProductList | 获取产品信息列表
EnableUIoTCoreDynamicRegister | 打开产品下设备动态注册功能
DisableUIoTCoreDynamicRegister | 禁用产品下设备动态注册
PublishUIoTCoreProduct | 发布产品
UnpublishUIoTCoreProduct | 撤销发布产品
ResetUIoTCoreProductPassword | 重置产品密钥



## 设备管理
API名称 | 描述
---|---
CreateUIoTCoreDevice | 创建物联网设备
ModifyUIoTCoreDevice | 修改物联网设备
DeleteUIoTCoreDevice | 删除设备
EnableUIoTCoreDevice | 启用设备
DisableUIoTCoreDevice | 禁用设备
BatchCreateUIoTCoreDevice | 批量创建物联网设备
BatchCreateUIoTCoreDeviceWithSN | 批量创建物联网设备
BatchDeleteUIoTCoreDevice | 批量删除设备
BatchEnableUIoTCoreDevice | 批量启用设备
BatchDisableUIoTCoreDevice | 批量禁用设备
GetUIoTCoreDeviceList | 获取设备列表
GetUIoTCoreInactivatedDevicePasswordFile | 获取未激活设备的密码文件


## 主题管理

API名称 | 描述
---|---
CreateUIoTCoreProductTopic | 创建产品Topic
ModifyUIoTCoreProductTopic | 修改产品Topic
DeleteUIoTCoreProductTopic | 删除产品Topic
GetUIoTCoreProductTopicList | 获取产品topic列表


## 设备影子

API名称 | 描述
---|---
EnableUIoTCoreDeviceShadow | 打开设备影子
DisableUIoTCoreDeviceShadow | 关闭设备影子
GetUIoTCoreDeviceShadow | 获取设备影子
UpdateUIoTCoreDeviceShadow | 更新设备影子文档


## 物模型

API名称 | 描述
---|---
AddUIoTCoreTModelProperty | 增加物模型属性
AddUIoTCoreTModelCommand | 添加物模型命令定义
AddUIoTCoreTModelEvent | 添加物模型事件定义
GetUIoTCoreDeviceProperty | 获取设备属性
GetUIoTCoreDeviceCommandList | 获取设备命令列表
GetUIoTCoreDeviceEventList | 获取设备事件列表
DeleteUIoTCoreTModelProperty | 删除物模型属性
DeleteUIoTCoreTModelCommand | 删除物模型命令定义
DeleteUIoTCoreTModelEvent | 删除物模型事件定义
ModifyUIoTCoreTModelProperty | 修改物模型属性
ModifyUIoTCoreTModelCommand | 修改物模型命令定义
ModifyUIoTCoreTModelEvent | 修改物模型事件定义
SetUIoTCoreDeviceProperty | 设置设备属性
SendUIoTCoreDeviceCommand | 发送命令
GetUIoTCoreTModelTemplate | 获取物模型定义模板


## 消息通信

API名称 | 描述
---|---
PublishUIoTCoreMQTTMessage | Publish MQTT消息
PublishUIoTCoreTDeviceMessage | Pub设备消息
BroadcastUIoTCoreMQTTMessage | 广播消息

## 规则引擎

API名称 | 描述
---|---
CreateUIoTCoreRule | 创建规则
GetUIoTCoreRuleList | 获取规则列表
ModifyUIoTCoreRule | 修改规则
DeleteUIoTCoreRule | 删除规则
EnableUIoTCoreRule | 启用规则
DisableUIoTCoreRule | 禁用规则
CreateUIoTCoreRuleAction | 创建规则Action
GetUIoTCoreRuleActionList | 获取规则Action列表
ModifyUIoTCoreRuleAction | 修改规则Action
DeleteUIoTCoreRuleAction | 删除规则Action



## 固件升级

API名称 | 描述
---|---
GetUIoTCoreUploadURL | 获取固件上传URL
DeleteUIoTCoreFirmware | 删除固件
UpdateUIoTCoreDeviceFW | 更新设备固件
BatchUpdateUIoTCoreDeviceFW | 批量更新设备固件
GetUIoTCoreDeviceVersionCount | 获取设备版本统计信息
GetUIoTCoreDeviceVersionList | 获取设备当前版本号列表
GetUIoTCoreFirmwareList | 获取固件列表
GetUIoTCoreFirmwareVersionList | 获取固件版本号列表
GetUIoTCoreUpdatableDeviceList | 获取可升级设备列表



## 监控与日志

API名称 | 描述
---|---
GetUIoTCoreLog | 获取日志信息
GetUIoTCoreMessageInfo | 获取消息信息
GetUIotCoreMetric | 获取状态监控数据
DescribeUiotCoreMetric | 监控信息

