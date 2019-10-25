{{indexmenu_n>10}}


# 规则引擎



## CreateUIoTCoreRule

创建规则

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleName|string|规则名称|**Yes**|
|ProductSN|string|产品序列号|No|
|DataType|string|数据类型 json或者binary|No|
|Description|string|规则描述|No|
|ShortTopic|string|应用规则的具体Topic|No|
|Select|string|要执行的Select语句(base64编码)|No|
|Where|string|规则触发条件(base64编码)|No|
|TopicType|string|topic类型，sys或者user|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|RuleID|string|规则ID|No|

### 请求示例
```
https://api.ucloud.cn/?Action=CreateUIoTCoreRule
&RuleName=rule_example
&ProductSN=biozpnofy3wpybua
&DataType=json
&Description=规则范例
&ShortTopic=/5q3ylz4jawrrog1c/upload
&Select=aWQ=
&Where=
&Region=cn-sh2
&TopicType=user
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreRuleResponse",
    "RuleID": "28"
}
```



## GetUIoTCoreRuleList

获取规则列表

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回最大数据长度，默认为20，最大为100|No|
|RuleID|string|规则ID，用于精确查询|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|TotalCount|int|总记录数|**Yes**|
|RuleSet|array[RuleSet]|规则列表信息|**Yes**|

### RuleSet 规则列表

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RuleName|string|规则名称|**Yes**|
|Status|string|状态|**Yes**|
|CreateTime|int|创建时间|**Yes**|
|DataType|string|数据类型|**Yes**|
|TopicType|string|topic类型，sys或者user|**Yes**|
|ProductSN|string|产品序列号|No|
|ShortTopic|string|应用规则的具体Topic|No|
|Description|string|规则描述|No|
|Select|string|要执行的Sql语句|No|
|Where|string|规则触发条件|No|
|RuleID|string|规则ID|No|

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreRuleList
&Offset=0
&Limit=100
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "TotalCount": 2,
    "RuleSet": [
        {
            CreateTime: 1564466988
            DataType: "json"
            Description: "2↵1↵2↵333343434343243434343434324324324324"
            ProductSN: "sp23xte8iebb43pu"
            RuleID: "14"
            RuleName: "testsms"
            Select: "id"
            ShortTopic: "/test1/upload/event"
            Status: "disabled"
            TopicType: "user"
        },
        {
            CreateTime: 1564392040
            DataType: "json"
            ProductSN: "12go9dakt4web4nw"
            RuleID: "6"
            RuleName: "qyr1"
            Select: "id,name"
            ShortTopic: "/qyr1/upload"
            Status: "running"
            TopicType: "user"
            Where: "id>0"
        }
    ],
    "RetCode": 0,
    "Action": "GetUIoTCoreRuleListResponse"
}
```



## ModifyUIoTCoreRule

修改规则

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|
|RuleName|string|修改后的规则名称|No|
|ProductSN|string|修改后的产品序列号|No|
|DataType|string|数据类型|No|
|Description|string|规则描述|No|
|ShortTopic|string|应用规则的具体Topic|No|
|Select|string|要执行的Sql语句(base64编码)|No|
|Where|string|规则触发条件(base64编码)|No|
|TopicType|string|topic类型，sys或者user|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=ModifyUIoTCoreRule
&RuleID=6
&RuleName=qyr1
&ProductSN=12go9dakt4web4nw
&DataType=json
&Description=规则范例新
&ShortTopic=/qyr1/upload
&Select=aWQsbmFtZQ==
&Where=aWQ+MA==
&Region=cn-sh2
&TopicType=user
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "ModifyUIoTCoreRuleResponse"
}
```



## DeleteUIoTCoreRule

删除规则

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=DeleteUIoTCoreRule
&RuleID=28
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DeleteUIoTCoreRuleResponse"
}
```



## EnableUIoTCoreRule

启用规则

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=EnableUIoTCoreRule
&RuleID=6
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "EnableUIoTCoreRuleResponse"
}
```



## DisableUIoTCoreRule

禁用规则

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=DisableUIoTCoreRule
&RuleID=6
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DisableUIoTCoreRuleResponse"
}
```



## CreateUIoTCoreRuleAction

创建规则Action

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|
|Type|string|规则Action的类型|**Yes**|
|Configuration|string|对应类型的配置(该字段要求按照base64编码)|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=CreateUIoTCoreRuleAction
&RuleID=6
&Type=mysql
&Configuration=eyJSZXNvdXJjZUlEIjoidWRiaGEtMHp0bzJnYmwiLCJSZXNvdXJjZU5hbWUiOiJ1aW90Y29yZS1wcm9kdWN0aW9uLWlvdGNvbmYiLCJQb3J0IjozMzA2LCJEYXRhYmFzZSI6ImlvdCIsIlRhYmxlIjoidGFibGUxIiwiVXNlcm5hbWUiOiJyb290IiwiUGFzc3dvcmQiOiJyb290IiwiRmllbGRzIjp7ImZpZWxkMSI6IiR7aWR9In19
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreRuleActionResponse"
}
```



## GetUIoTCoreRuleActionList

获取规则Action列表

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回最大数据长度，默认为20，最大为100|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|TotalCount|int|总记录数|**Yes**|
|RuleActionSet|array[RuleActionSet]|规则列表信息|**Yes**|

### RuleActionSet 规则Action列表

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|ActionID|string|规则Action ID|**Yes**|
|Type|string|规则Action 类型|**Yes**|
|Configuration|string|对应类型的配置|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreRuleActionList
&RuleID=6
&Offset=0
&Limit=100
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "TotalCount": 2,
    "RuleActionSet": [
        {
            ActionID: "41"
            Configuration: "{"ResourceID":"uhost-u3xfb5co","ResourceName":"ubuntu-vnc","Port":9090,"Path":"/hello"}"
            Type: "http"
        },
        {
           ActionID: "6"
            Configuration: "{"TopicType":"user","Topic":"/12go9dakt4web4nw/qyr1/set"}"
            Type: "republish"
        }
    ],
    "RetCode": 0,
    "Action": "GetUIoTCoreRuleActionListResponse"
}
```



## ModifyUIoTCoreRuleAction

修改规则Action

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|
|ActionID|string|Action ID|**Yes**|
|Type|string|规则Action的类型|**Yes**|
|Configuration|string|对应类型的配置(base64编码)|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=ModifyUIoTCoreRuleAction
&RuleID=6
&ActionID=41
&Type=http
&Configuration=eyJSZXNvdXJjZUlEIjoidWhvc3QtdTN4ZmI1Y28iLCJSZXNvdXJjZU5hbWUiOiJ1YnVudHUtdm5jIiwiUGF0aCI6Ii9oZWxsbyIsIlBvcnQiOjkwOTB9
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "ModifyUIoTCoreRuleActionResponse"
}
```



## DeleteUIoTCoreRuleAction

删除规则Action

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|RuleID|string|规则ID|**Yes**|
|ActionID|string|规则Action ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=DeleteUIoTCoreRuleAction
&RuleID=6
&ActionID=6
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DeleteUIoTCoreRuleActionResponse"
}
```
