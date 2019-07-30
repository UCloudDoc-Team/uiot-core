{{indexmenu_n>7}}

# 设备影子



## EnableUIoTCoreDeviceShadow

打开设备影子

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|**Yes**|
|ProductSN|string|产品ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Timestamp|string|操作时间戳|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=EnableUIoTCoreDeviceShadow
&Region=cn-zj
&ProjectId=kXsyKClX
&ProductSN=ulFbNbcr
```
### 响应示例
```
{
    "Timestamp": "ZaEHdWsS",
    "RetCode": 0,
    "Action": "EnableUIoTCoreDeviceShadowResponse"
}
```




## DisableUIoTCoreDeviceShadow

关闭设备影子

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|**Yes**|
|ProductSN|string|产品ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Timestamp|string|操作时间戳|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=DisableUIoTCoreDeviceShadow
&Region=cn-zj
&ProjectId=aDeEFNtg
&ProductSN=QCCSxGIJ
```
### 响应示例
```
{
    "Timestamp": "xBdMlaya",
    "RetCode": 0,
    "Action": "DisableUIoTCoreDeviceShadowResponse"
}
```




## GetUIoTCoreDeviceShadow

获取设备影子文档

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|**Yes**|
|ProductSN|string|产品ID|**Yes**|
|DeviceSN|string|设备ID|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Payload|object|数据载荷|**Yes**|
|Version|int|设备影子版本好|**Yes**|
|Timestamp|string|操作时间戳|**Yes**|

### Payload 数据载荷

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|State|object|设备影子State字段|**Yes**|
|Metadata|object|设备影子Metadata字段|**Yes**|

### State 设备影子文档

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Reported|object|设备上报的状态|No|
|Desired|object|应用下发的状态|No|

### Metadata 设备影子文档操作时间戳

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Reported|object|设备上报的状态时间戳|No|
|Desired|object|应用下发的状态时间戳|No|


### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreDeviceShadow
&Region=cn-zj
&ProjectId=wZnGKFpc
&ProductSN=myYJTQTR
&DeviceSN=XlNkDkHw
```
### 响应示例
```
{
    "Payload": {},
    "Version": 1,
    "Timestamp": "dNktleTJ",
    "RetCode": 0,
    "Action": "GetUIoTCoreDeviceShadowResponse"
}
```




## UpdateUIoTCoreDeviceShadow

更新设备影子文档

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](../summary/regionlist.html)|**Yes**|
|ProjectId|string|项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html)|**Yes**|
|Desired|string|base64编码的Json字符串|**Yes**|
|ProductSN|string|产品ID|**Yes**|
|DeviceSN|string|设备ID|**Yes**|
|ShadowVersion|string|设备影子版本|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Payload|object|数据载荷|No|
|Version|int|设备影子文档|No|
|Timestamp|string|操作时间戳|No|

### Payload 数据载荷

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|State|object|设备影子State字段|**Yes**|
|Metadata|object|设备影子Metadata字段|**Yes**|

### State 设备影子文档

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Reported|object|设备上报的状态|No|
|Desired|object|应用下发的状态|No|

### Metadata 设备影子文档操作时间戳

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Reported|object|设备上报的状态时间戳|No|
|Desired|object|应用下发的状态时间戳|No|



### 请求示例
```
https://api.ucloud.cn/?Action=UpdateUIoTCoreDeviceShadow
&Region=cn-zj
&ProjectId=xVqvjzSS
&Desired=bFcfVbbn
&ProductSN=PFmsLErG
&DeviceSN=FDRHHEQN
&Version=5
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "UpdateUIoTCoreDeviceShadowResponse",
    "Payload": {},
    "Version": 9,
    "Timestamp": "FGLKHDLd"
}
```