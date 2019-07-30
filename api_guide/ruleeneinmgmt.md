{{indexmenu_n>10}}


# 规则引擎



## CreateUIoTCoreRule

创建规则

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|RuleName|string|规则名称|**Yes**|
|ProductSN|string|产品序列号|No|
|DataType|string|数据类型 json或者binary|No|
|Description|string|规则描述|No|
|ShortTopic|string|应用规则的具体Topic|No|
|Select|string|要执行的Select语句|No|
|Where|string|规则触发条件|No|
|TopicType|string|topic类型，sys还是user|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|RuleID|string|规则ID|No|

### 请求示例
```
https://api.ucloud.cn/?Action=CreateUIoTCoreRule
&RuleName=PAtNOOqG
&ProductSN=upwHohgS
&DataType=jZEBiBwB
&Description=cbJDLoOB
&ShortTopic=DtKwCVaz
&Select=bjScgcES
&Where=EKspFljR
&ProjectId=mSiNqbNj
&Region=mHTWGUew
&TopicType=nwDykwnp
&TopicType=hPCJVmDh
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreRuleResponse",
    "RuleID": "RjLLMyOP"
}
```



## GetUIoTCoreRuleList

获取规则列表-GetUIoTCoreRuleList

获取规则列表

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
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
&Offset=2
&Limit=50
&ProjectId=bXapdQku
&Region=PbAhGDOC
&RuleID=7
&RuleID=TIECLnai
```
### 响应示例
```
{
    "TotalCount": 2,
    "RuleSet": [
        {
            "ProductSN": "GEnnlVPh",
            "RuleName": "WEYzcpnq",
            "Status": "SlMWBWAB",
            "CreateTime": 2,
            "DataType": "AfACJskp",
            "ShortTopic": "GpLCzKwY",
            "Description": "pIptYAZp",
            "Select": "lBjDFqFd",
            "Where": "BqFIJNkg",
            "RuleID": "rZtpTMsQ"
        },
        {
            "ProductSN": "tUzcWqbQ",
            "RuleName": "AgupeZyB",
            "Status": "rGamrUcV",
            "CreateTime": 2,
            "DataType": "mACLvySR",
            "ShortTopic": "DPkrPSSv",
            "Description": "cwmDtOsE",
            "Select": "jEJmXkMx",
            "Where": "KucLLkUa",
            "RuleID": "lYHjLkgA"
        },
        {
            "ProductSN": "TAXtRTDq",
            "RuleName": "eqQbOVzH",
            "Status": "LJlcqaVI",
            "CreateTime": 3,
            "DataType": "bvUEJIWc",
            "ShortTopic": "rvQbMepO",
            "Description": "uphmalel",
            "Select": "HHSchvuI",
            "Where": "ZxZYevzp",
            "RuleID": "BkojlXYW"
        },
        {
            "ProductSN": "VsptRcHO",
            "RuleName": "VhsgziXZ",
            "Status": "IBdzOpok",
            "CreateTime": 5,
            "DataType": "nOgRWjks",
            "ShortTopic": "lPhdlQir",
            "Description": "AGAzBlJK",
            "Select": "aCzqOjbI",
            "Where": "xqKBmlMp",
            "RuleID": "AwhGXJSP"
        },
        {
            "ProductSN": "RtdUgImw",
            "RuleName": "fvVlCMHI",
            "Status": "LCiWQEVa",
            "CreateTime": 6,
            "DataType": "FlhhHZCL",
            "ShortTopic": "iOGefDQs",
            "Description": "TvOKrSjD",
            "Select": "XhFAnTGB",
            "Where": "yfECEOlB",
            "RuleID": "LPxiVUMs"
        },
        {
            "ProductSN": "yaugcgrV",
            "RuleName": "CacKmqPv",
            "Status": "UeLgtGAR",
            "CreateTime": 3,
            "DataType": "RReNVTMW",
            "ShortTopic": "lzPqswzr",
            "Description": "DNFsclxj",
            "Select": "VHtbOOeg",
            "Where": "yzgzVPZH",
            "RuleID": "EKgNNwYC"
        },
        {
            "ProductSN": "uliGYCLm",
            "RuleName": "SBEniHkh",
            "Status": "PxwpHdXK",
            "CreateTime": 1,
            "DataType": "wVHKkiBk",
            "ShortTopic": "eExlQCBP",
            "Description": "FjPIwYNy",
            "Select": "UrlciCbN",
            "Where": "WbhZWuMk",
            "RuleID": "hNdHRKcA"
        },
        {
            "ProductSN": "KiAXhiIc",
            "RuleName": "HDJbOITS",
            "Status": "tFipUgHl",
            "CreateTime": 6,
            "DataType": "miVVGGkU",
            "ShortTopic": "hJKRoghd",
            "Description": "voCBPsIA",
            "Select": "UmJlMjmV",
            "Where": "RPfsEycb",
            "RuleID": "lhfMhlMR"
        },
        {
            "ProductSN": "XaAPFabx",
            "RuleName": "IahwPnGt",
            "Status": "RacydrMU",
            "CreateTime": 7,
            "DataType": "ocUJDcMf",
            "ShortTopic": "wraJPGRB",
            "Description": "PdWtIfmg",
            "Select": "FGZKBmqk",
            "Where": "oNqpMBKk",
            "RuleID": "ZmeSmJYm"
        },
        {
            "ProductSN": "LKvrgRoI",
            "RuleName": "APOGTFjN",
            "Status": "TJaxzVqr",
            "CreateTime": 1,
            "DataType": "amQUyBYo",
            "ShortTopic": "sdVbtJFR",
            "Description": "jSSmTZvR",
            "Select": "aphtimcy",
            "Where": "wpNxHiRc",
            "RuleID": "bPIXupPZ"
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|RuleID|string|规则ID|**Yes**|
|RuleName|string|修改后的规则名称|No|
|ProductSN|string|修改后的产品序列号|No|
|DataType|string|数据类型|No|
|Description|string|规则描述|No|
|ShortTopic|string|应用规则的具体Topic|No|
|Select|string|要执行的Sql语句|No|
|Where|string|规则触发条件|No|
|TopicType|string|topic类型，sys或者user|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=ModifyUIoTCoreRule
&RuleID=EcidGqGP
&RuleName=pQbiorTk
&ProductSN=QRAevXFd
&DataType=kisEmrGc
&Description=JNsZbbql
&ShortTopic=rhBBhnOL
&Select=ZSInWfsO
&Where=FxJKxhKF
&ProjectId=dWXaLHNA
&Region=uJjOytFX
&TopicType=lQnDEPUp
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|RuleID|string|规则ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=DeleteUIoTCoreRule
&RuleID=viKxxAaG
&ProjectId=WkRimFta
&Region=mthRKOdw
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|RuleID|string|规则ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=EnableUIoTCoreRule
&RuleID=DASXntnV
&ProjectId=eHwaKSCJ
&Region=vYrUleNN
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|RuleID|string|规则ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=DisableUIoTCoreRule
&RuleID=LrraFMTS
&ProjectId=dAqklloE
&Region=rRPEPckg
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|RuleID|string|规则ID|**Yes**|
|Type|string|规则Action的类型|**Yes**|
|Configuration|string|对应类型的配置(该字段要求按照url.encode编码)|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=CreateUIoTCoreRuleAction
&RuleID=UHjOaeMw
&Type=vpYvXdTf
&Configuration=aYKBQRqB
&ProjectId=qPhuZczR
&Region=rLrLSFVe
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
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
&RuleID=gsVmTRPC
&Offset=7
&Limit=2
&ProjectId=aiLFdQnU
&Region=ebdIVIMf
```
### 响应示例
```
{
    "TotalCount": 5,
    "RuleActionSet": [
        {
            "ActionID": "WJEuPYDP",
            "Type": "sBnZroTk",
            "Configuration": "UkTCfyOg"
        },
        {
            "ActionID": "arZztkqm",
            "Type": "xqfjdoTp",
            "Configuration": "DffkEhGo"
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
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|RuleID|string|规则ID|**Yes**|
|ActionID|string|Action ID|**Yes**|
|Type|string|规则Action的类型|**Yes**|
|Configuration|string|对应类型的配置|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=ModifyUIoTCoreRuleAction
&RuleID=ZFYIuYdb
&ActionID=vnrGkmre
&Type=RjWrgrvl
&Configuration=rByVnmIV
&ProjectId=VyjYFMnF
&Region=vzXomSVe
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "ModifyUIoTCoreRuleActionResponse",
    "Test": {}
}
```



## DeleteUIoTCoreRuleAction

删除规则Action

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
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
&RuleID=xnpbnrfM
&ActionID=jNqkpIyt
&ProjectId=GNNFZtRg
&Region=vvJxEIAs
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DeleteUIoTCoreRuleActionResponse"
}
```
