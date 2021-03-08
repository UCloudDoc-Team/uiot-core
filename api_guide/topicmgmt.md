# 主题管理



## CreateUIoTCoreProductTopic

创建产品Topic

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|Topic|string|产品Topic名称|**Yes**|
|Permission|string|Topic权限，默认为sub，合法值为: sub,pub,pubsub|**Yes**|
|Description|string|Topic描述|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=CreateUIoTCoreProductTopic
&ProductSN=7ab051kbfhhjakc0
&Topic=/7ab051kbfhhjakc0/${DeviceSN}/hello
&Permission=sub
&Description=hello
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreProductTopicResponse"
}
```




## ModifyUIoTCoreProductTopic

修改产品Topic

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|Topic|string|Topic名称|**Yes**|
|NewTopic|string|修改后的Topic名称|No|
|NewPermission|string|修改后的Topic权限，合法值为: sub,pub,pubsub|No|
|NewDescription|string|修改后的Topic描述|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=ModifyUIoTCoreProductTopic
&ProductSN=7ab051kbfhhjakc0
&Topic=/7ab051kbfhhjakc0/${DeviceSN}/hello
&NewTopic=/7ab051kbfhhjakc0/${DeviceSN}/world
&NewPermission=pubsub
&NewDescription=world
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "ModifyUIoTCoreProductTopicResponse"
}
```




## DeleteUIoTCoreProductTopic

删除产品Topic

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|Topic|string|产品Topic|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=DeleteUIoTCoreProductTopic
&ProductSN=7ab051kbfhhjakc0
&Topic=/7ab051kbfhhjakc0/${DeviceSN}/world
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DeleteUIoTCoreProductTopicResponse"
}
```




## GetUIoTCoreProductTopicList

获取产品topic列表

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回最大数据长度，默认为20，最大为100|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|TotalCount|int|总记录数|**Yes**|
|TopicSet|array[TopicSet]|Topic列表|**Yes**|

### TopicSet 产品topic列表

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Topic|string|Topic名称|**Yes**|
|Permission|string|权限 取pub、sub或pubsub|**Yes**|
|Type|string|topic类型, sys或者user|**Yes**|
|RuleEnginePermission|string|规则引擎权限 pub, sub或者pubsub|**Yes**|
|Description|string|Topic描述|No|

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreProductTopicList
&ProductSN=7ab051kbfhhjakc0
&Offset=0
&Limit=100
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "Action":"GetUIoTCoreProductTopicListResponse",
    "RetCode":0,
    "TopicSet":[
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/device/status",
            "Permission":"-",
            "Description":"设备状态变化(仅供规则引擎订阅)",
            "Type":"sys",
            "RuleEnginePermission":"sub"
        },
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/shadow/document",
            "Permission":"-",
            "Description":"设备影子发生变化时将发送完整的设备影子文档(仅供规则引擎订阅)",
            "Type":"sys",
            "RuleEnginePermission":"sub"
        },
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/tmodel/command",
            "Permission":"sub",
            "Description":"下发物模型命令到设备",
            "Type":"sys",
            "RuleEnginePermission":"pub"
        },
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/tmodel/command_reply/+",
            "Permission":"pub",
            "Description":"设备回复物模型命令",
            "Type":"sys",
            "RuleEnginePermission":"sub"
        },
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/tmodel/event/post",
            "Permission":"pub",
            "Description":"设备上报物模型事件",
            "Type":"sys",
            "RuleEnginePermission":"sub"
        },
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/tmodel/property/document",
            "Permission":"-",
            "Description":"设备的物模型属性发生变化时将发送完整的物模型属性文档(仅供规则引擎订阅)",
            "Type":"sys",
            "RuleEnginePermission":"sub"
        },
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/tmodel/property/post",
            "Permission":"pub",
            "Description":"设备上报物模型属性",
            "Type":"sys",
            "RuleEnginePermission":"sub"
        },
        {
            "Topic":"/$system/7ab051kbfhhjakc0/${DeviceSN}/tmodel/property/set",
            "Permission":"sub",
            "Description":"设备接受物模型属性设置",
            "Type":"sys",
            "RuleEnginePermission":"pub"
        },
        {
            "Topic":"/7ab051kbfhhjakc0/${DeviceSN}/upload/event",
            "Permission":"pub",
            "Type":"user",
            "RuleEnginePermission":"pubsub"
        },
        {
            "Topic":"/7ab051kbfhhjakc0/${DeviceSN}/upload",
            "Permission":"pub",
            "Type":"user",
            "RuleEnginePermission":"pubsub"
        },
        {
            "Topic":"/7ab051kbfhhjakc0/${DeviceSN}/set",
            "Permission":"sub",
            "Type":"user",
            "RuleEnginePermission":"pubsub"
        }
    ],
    "TotalCount":11
}
```

