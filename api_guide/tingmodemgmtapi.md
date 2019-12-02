# 物模型

## GetUIoTCoreDeviceProperty

获取设备属性值

### 请求参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|

### 响应参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Status|string|设备状态|**Yes**|
|LatestUpdateTime|string|最近更新时间, 毫秒时间戳|**Yes**|
|Property|object|物模型属性信息|No|

### 请求示例

```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreDeviceProperty
&Region=cn-sh2
&ProductSN=sp23xte8iebb43pu
&DeviceSN=test1
&公共请求参数
```

### 响应示例

```
{
  "Action": "GetUIoTCoreDevicePropertyResponse",
  "RetCode": 0,
  "Status": "online",
  "LatestUpdateTime": "1564541969775",
  "Property": {
    "volume": {
      "Time": 1564541969775,
      "Value": 50
    }
  }
}
```

## GetUIoTCoreDeviceCommandList

获取设备命令记录列表

### 请求参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回最大数据长度，-1表示返回所有，默认为-1|No|
|StartTime|int|开始时间戳（秒），默认为0|No|
|EndTime|int|结束时间戳（秒），默认为当前时间戳|No|
|Identifier|string|标识符，默认为全部标识符|No|
|RequestID|string|请求ID，默认为全部请求ID|No|

### 响应参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|TotalCount|int|命令记录总数|**Yes**|
|CommandSet|array[CommandSet]|命令记录列表|**Yes**|

### CommandSet 命令列表单元

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RequestID|string|请求ID|**Yes**|
|Identifier|string|标识符|**Yes**|
|Name|string|名称|**Yes**|
|Time|int|毫秒时间戳|**Yes**|
|Input|object|命令输入|**Yes**|
|Output|object|命令输出|**Yes**|
|Result|string|命令执行结果|**Yes**|

### 请求示例

```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreDeviceCommandList
&Region=cn-sh2
&ProductSN=sp23xte8iebb43pu
&DeviceSN=test1
&Offset=0
&Limit=10
&StartTime=1564539339
&EndTime=1564542939
&公共请求参数
```

### 响应示例

```
{
  "Action": "GetUIoTCoreDeviceCommandListResponse",
  "RetCode": 0,
  "TotalCount": 1,
  "CommandSet": [
    {
      "RequestID": "341051897566314496",
      "Identifier": "download_music",
      "Time": "1564541908817",
      "Name": "下载音乐",
      "Input": {
        "url": "www.ucloud.cn"
      },
      "Output": {
        "result": 1
      },
      "Result": "success"
    }
  ]
}
```

## GetUIoTCoreDeviceEventList

获取设备事件记录列表

### 请求参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回数据长度，默认为-1，-1表示返回所有|No|
|StartTime|int|开始时间戳（秒），默认为0|No|
|EndTime|int|结束时间戳（秒），默认为当前时间戳|No|
|Identifier|string|标识符，默认为所有标识符|No|
|RequestID|string|请求ID，默认为全部请求ID|No|

### 响应参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|TotalCount|int|事件记录总数|**Yes**|
|EventSet|array[EventSet]|事件记录列表|**Yes**|

### EventSet 事件列表单元

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RequestID|string|请求ID|**Yes**|
|Identifier|string|标识符|**Yes**|
|Name|string|名称|**Yes**|
|Type|string|事件类型|**Yes**|
|Time|string|毫秒时间戳|**Yes**|
|Output|object|事件输出|**Yes**|

### 请求示例

```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreDeviceEventList
&Region=cn-sh2
&ProductSN=sp23xte8iebb43pu
&DeviceSN=test1
&Offset=0
&Limit=10
&StartTime=1564539797
&EndTime=1564543397
&公共请求参数
```

### 响应示例

```
{
  "Action": "GetUIoTCoreDeviceEventListResponse",
  "RetCode": 0,
  "TotalCount": 1,
  "EventSet": [
    {
      "RequestID": "1",
      "Identifier": "low_power_alert",
      "Name": "低电量告警",
      "Type": "warning",
      "Time": "1564541812810",
      "Output": {
        "power": 5
      }
    }
  ]
}
```

## SetUIoTCoreDeviceProperty

设置设备属性

### 请求参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
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
https://api-cn-sh2.iot.ucloud.cn/?Action=SetUIoTCoreDeviceProperty
&Region=cn-sh2
&ProductSN=sp23xte8iebb43pu
&DeviceSN=test1
&Property=eyJ2b2x1bWUiOjkwfQ==
&Desired=false
&公共请求参数
```

### 响应示例

```
{
  "Action": "SetUIoTCoreDevicePropertyResponse",
  "RetCode": 0,
  "RequestID": "341086531714285568"
}
```

## SendUIoTCoreDeviceCommand

发送命令

### 请求参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
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
https://api-cn-sh2.iot.ucloud.cn/?Action=SendUIoTCoreDeviceCommand
&Region=cn-sh2
&ProductSN=sp23xte8iebb43pu
&DeviceSN=test1
&Identifier=download_music
&Input=eyJ1cmwiOiJ3d3cudWNsb3VkLmNuIn0=
&Method=async
&Timeout=5
&公共请求参数
```

### 响应示例

```
{
  "Action": "SendUIoTCoreDeviceCommandResponse",
  "RetCode": 0,
  "RequestID": "341085313453522945",
  "Output": {}
}
```

## GetUIoTCoreTModelTemplate

获取物模型定义模板

### 请求参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|

### 响应参数

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|Template|object|物模型定义|**Yes**|

### 请求示例

```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreTModelTemplate
&Region=cn-sh2
&ProductSN=sp23xte8iebb43pu
&公共请求参数
```

### 响应示例

```
{
  "Action": "GetUIoTCoreTModelTemplateResponse",
  "RetCode": 0,
  "Template": {
    "Property": [
      {
        "PropertyID": 9,
        "Identifier": "volume",
        "Name": "音量",
        "AccessMode": "rw",
        "Description": "智能音箱音量，数值表示音量百分比",
        "DataType": {
          "Type": "int32",
          "Spec": {
            "Max": 100,
            "Min": 0,
            "Step": 1,
            "UnitName": ""
          }
        }
      }
    ],
    "Event": [
      {
        "EventID": 21,
        "Identifier": "low_power_alert",
        "Name": "低电量告警",
        "Type": "warning",
        "Description": "当电量小于10%触发低电量告警",
        "Output": [
          {
            "Identifier": "power",
            "Name": "电量百分比",
            "DataType": {
              "Type": "int32",
              "Spec": {
                "Max": 10,
                "Min": 0,
                "Step": 1,
                "UnitName": ""
              }
            }
          }
        ]
      }
    ],
    "Command": [
      {
        "CommandID": 12,
        "Identifier": "download_music",
        "Name": "下载音乐",
        "Description": "控制智能音箱从指定URL下载音乐资源",
        "Input": [
          {
            "Identifier": "url",
            "Name": "音乐资源URL",
            "DataType": {
              "Type": "string",
              "Spec": {
                "Length": 255
              }
            }
          }
        ],
        "Output": [
          {
            "Identifier": "result",
            "Name": "执行结果",
            "DataType": {
              "Type": "bool",
              "Spec": {
                "0": "执行失败",
                "1": "执行成功"
              }
            }
          }
        ]
      }
    ]
  }
}
```
