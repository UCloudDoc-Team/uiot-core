{{indexmenu_n>6}}


# 主题管理



## CreateUIoTCoreProductTopic

创建产品Topic

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|No|
|ProductSN|string|产品序列号|**Yes**|
|Topic|string|产品Topic名称|**Yes**|
|Permission|string|Topic权限，默认为sub，合法值为: sub,pub,pubsub|No|
|Description|string|Topic描述|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=CreateUIoTCoreProductTopic
&ProductSN=wqUFnaHP
&Topic=iWrvztwc
&Permission=ioRZVMXq
&Description=lKcqHTgJ
&ProjectId=TgKGkjJw
&Region=CkfSGPMW
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
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|No|
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
https://api.ucloud.cn/?Action=ModifyUIoTCoreProductTopic
&ProductSN=FCScQghj
&Topic=ZXEFZKns
&NewTopic=aqvXxDfx
&NewPermission=rjAXIEFu
&NewDescription=ywwroxzE
&ProjectId=PRtEeCUG
&Region=PziWucbA
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
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|No|
|ProductSN|string|产品序列号|**Yes**|
|Topic|string|产品Topic|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=DeleteUIoTCoreProductTopic
&ProductSN=XDbBSyNg
&Topic=zizullnm
&ProjectId=QcEUDfXF
&Region=NKmHjaEu
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
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|No|
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
https://api.ucloud.cn/?Action=GetUIoTCoreProductTopicList
&ProductSN=ttHYkaQH
&Offset=2
&Limit=3
&ProjectId=gChTfqoc
&Region=DhBozWeo
```
### 响应示例
```
{
    "TotalCount": 6,
    "TopicSet": [
        {
            "Topic": "oahkVaNc",
            "Permission": "EtqUOLbN",
            "Description": "QcpwKCLS"
        },
        {
            "Topic": "NiLWYiFm",
            "Permission": "TwSJJsEX",
            "Description": "EHmjijhF"
        },
        {
            "Topic": "PFSzDqZp",
            "Permission": "aUlAgkeC",
            "Description": "CyXMutgU"
        }
    ],
    "RetCode": 0,
    "Action": "GetUIoTCoreProductTopicListResponse"
}
```

