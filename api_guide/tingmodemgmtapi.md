{{indexmenu_n>8}}


# 物模型



## GetUIoTCoreDeviceProperty

获取设备属性

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|Zone|string|可用区。参见 [可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Status|string|设备状态|**Yes**|
|LatestUpdateTime|string|最近更新时间|**Yes**|
|Property|object|属性|No|
|Message|string|错误信息|No|

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreDeviceProperty
&Region=cn-zj
&Zone=cn-zj-01
&ProjectId=GMPmBEAN
&ProductSN=aDkMOSOr
&DeviceSN=ZBCvCLik
```
### 响应示例
```
{
    "Status": "rPFrYOPy",
    "LatestUpdateTime": "sfWtQPLZ",
    "RetCode": 0,
    "Action": "GetUIoTCoreDevicePropertyResponse",
    "Property": {},
    "Message": "qlLOfGdw"
}
```




## GetUIoTCoreDeviceCommandList

获取设备命令列表

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回最大数据长度，-1表示返回所有，默认为-1|No|
|StartTime|int|开始时间戳，默认为0|No|
|EndTime|int|结束时间戳，默认为当前时间戳|No|
|Identifier|string|标识符，默认为全部标识符|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|TotalCount|int|命令记录总数|**Yes**|
|CommandSet|array[CommandSet]|命令列表|**Yes**|

### CommandSet 命令列表单元

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RequestID|string|请求ID|**Yes**|
|Identifier|string|标识符|**Yes**|
|Name|string|名称|**Yes**|
|Time|int|时间戳|**Yes**|
|Input|object|输入|**Yes**|
|Output|object|输出|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreDeviceCommandList
&Region=cn-zj
&ProjectId=LxXTzBbh
&ProductSN=aDnSmEUp
&DeviceSN=sEjiWIQt
&Offset=2
&Limit=6
&StartTime=RoeeMtZR
&EndTime=EKEXQGeD
&Identifier=lBOCZozC
&StartTime=NBhFPJsE
&EndTime=HFsLbbZj
&Identifier=OSLzdSvb
```
### 响应示例
```
{
    "TotalCount": 7,
    "CommandSet": [
        "wOolMPoG"
    ],
    "RetCode": 0,
    "Action": "GetUIoTCoreDeviceCommandListResponse"
}
```




## GetUIoTCoreDeviceEventList

获取设备事件列表

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回数据长度，默认为-1，-1表示返回所有	|No|
|StartTime|int|开始时间戳，默认为0|No|
|EndTime|int|结束时间戳，默认为当前时间戳|No|
|Identifier|string|标识符，默认为所有标识符|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|TotalCount|int|事件总数|**Yes**|
|EventSet|array[EventSet]|事件列表|**Yes**|

### EventSet 事件列表单元

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RequestID|string|请求ID|**Yes**|
|Identifier|string|标识符|**Yes**|
|Name|string|名称|**Yes**|
|Time|string|时间戳，精确到毫秒|**Yes**|
|Output|object|输出|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreDeviceEventList
&Region=cn-zj
&ProjectId=aXhYxmNX
&ProductSN=QOgYZsSH
&DeviceSN=CWOmWreW
&Offset=7
&Limit=5
&StartTime=3
&EndTime=3
&Identifier=gaOBIPMS
```
### 响应示例
```
{
    "TotalCount": 5,
    "EventSet": [
        7
    ],
    "RetCode": 0,
    "Action": "GetUIoTCoreDeviceEventListResponse"
}
```




## SetUIoTCoreDeviceProperty

设置设备属性

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|Zone|string|可用区。参见 [可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|Property|string|属性列表，为base64之后的json字符串，json串的格式为{"PropertyIdentifier":PropertyValue}|**Yes**|
|Desired|bool|设备不在线时是否缓存云端，默认为false|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|RequestID|string|请求ID|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=SetUIoTCoreDeviceProperty
&Region=cn-zj
&Zone=cn-zj-01
&ProjectId=oSRhbNWe
&ProductSN=QaKjfFIO
&DeviceSN=TtsGAefv
&Property=MbQcwaOy
&Desired=true
```
### 响应示例
```
{
    "RequestID": "OHiyZHos",
    "RetCode": 0,
    "Action": "SetUIoTCoreDevicePropertyResponse"
}
```



## SendUIoTCoreDeviceCommand

发送命令

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|No|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|Identifier|string|标识符|**Yes**|
|Input|string|base64后的json字符串，格式参考物模型模板。默认为空|No|
|Method|string|sync或者async。默认为async|No|
|Timeout|int|超时时间，单位为秒，只在method为sync时有效，最长不超过5秒。默认为5|No|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|RequestID|string|请求ID|**Yes**|
|Output|object|输出|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=SendUIoTCoreDeviceCommand
&Region=cn-zj
&ProjectId=BJVVVaIu
&ProductSN=hwNiMubW
&DeviceSN=ILZMtZTC
&Identifier=jYkmMSar
&Input=BXkdiLXA
&Method=eHxaKIIp
&Timeout=8
```
### 响应示例
```
{
    "RequestID": "RllEjfYI",
    "Output": {},
    "RetCode": 0,
    "Action": "SendUIoTCoreDeviceCommandResponse"
}
```




## GetUIoTCoreTModelTemplate

获取物模型定义模板

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|Zone|string|可用区。参见 [可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](https://docs.ucloud.cn/api/summary/get_project_list)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Template|object|物模型定义|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreTModelTemplate
&Region=cn-zj
&Zone=cn-zj-01
&ProjectId=BptczDXE
&ProductSN=ZuSVPrHC
```
### 响应示例
```
{
    "Template": {},
    "RetCode": 0,
    "Action": "GetUIoTCoreTModelTemplateResponse"
}
```

