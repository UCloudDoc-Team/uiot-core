# 设备影子



## EnableUIoTCoreDeviceShadow

打开设备影子

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
| Region  | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist) |  **Yes** |
| ProductSN      | string | 产品ID                                                       |  **Yes** |



### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Timestamp|string|操作时间戳|**Yes**|

### 请求示例
```
https://api.ucloud.cn/?Action=EnableUIoTCoreDeviceShadow
&Region=cn-sh2
&ProductSN=ulFbNbcr
&公共请求参数
```
### 响应示例
```
{
    "Timestamp": "1564543200",
    "RetCode": 0,
    "Action": "EnableUIoTCoreDeviceShadowResponse"
}
```




## DisableUIoTCoreDeviceShadow

关闭设备影子

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
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
&Region=cn-sh2
&ProductSN=QCCSxGIJ
&公共请求参数
```
### 响应示例
```
{
    "Timestamp": "1564543200",
    "RetCode": 0,
    "Action": "DisableUIoTCoreDeviceShadowResponse"
}
```




## GetUIoTCoreDeviceShadow

获取设备影子文档

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
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
&Region=cn-sh2
&ProductSN=myYJTQTR
&DeviceSN=XlNkDkHw
&公共请求参数
```
### 响应示例
```
{
	"Action": "GetUIoTCoreDeviceShadowResponse",
	"RetCode": 0,
	"Payload": {
		"State": {
			"Reported": {
				"light": "on"
			},
			"Desired": {
				"key": "value",
				"key_1": "value_1"
			}
		},
		"Metadata": {
			"Reported": {
				"light": {
					"Timestamp": 1564395928
				}
			},
			"Desired": {
				"key": {
					"Timestamp": 1564399417
				},
				"key_1": {
					"Timestamp": 1564557762
				}
			}
		}
	},
	"Version": 8,
	"Timestamp": 1564557762
}
```




## UpdateUIoTCoreDeviceShadow

更新设备影子文档

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
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
&Region=cn-sh2
&Desired=eyJrZXlfMSI6InZhbHVlXzEifQ==
&ProductSN=PFmsLErG
&DeviceSN=FDRHHEQN
&Version=5
&公共请求参数
```
### 响应示例
```
{
	"RetCode": 0,
	"Action": "UpdateUIoTCoreDeviceShadowResponse",
	"Payload": {
		"State": {
			"Reported": {
				"light": "on"
			},
			"Desired": {
				"key": "value",
				"key_1": "value_1"
			}
		},
		"Metadata": {
			"Reported": {
				"light": {
					"Timestamp": 1564395928
				}
			},
			"Desired": {
				"key": {
					"Timestamp": 1564399417
				},
				"key_1": {
					"Timestamp": 1564399352
				}
			}
		}
	},
	"Version": 9,
	"Timestamp": "1564543200"
}
```