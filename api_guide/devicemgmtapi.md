# 设备管理



## CreateUIoTCoreDevice

创建物联网设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号，不填则由系统自动生成                             |       No |
| Description    | string | 设备描述信息                                                 |       No |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |
| Password       | string | 设备密钥    |       No |
| DeviceSN       | string | 设备序列号  |       No |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=CreateUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN=h6phdnkjvr90iq6l
&Description=灯泡1
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreDeviceResponse",
    "Password": "r23xnp8pet765dr4",
    "DeviceSN": "h6phdnkjvr90iq6l"
}
```



## ModifyUIoTCoreDevice

修改物联网设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号                                                   |  **Yes** |
| NewDescription | string | 修改后的设备描述                                             |       No |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=ModifyUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN=h6phdnkjvr90iq6l
&NewDescription=light1
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "ModifyUIoTCoreDeviceResponse"
}
```



## DeleteUIoTCoreDevice

删除设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=DeleteUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN=h6phdnkjvr90iq6l
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DeleteUIoTCoreDeviceResponse"
}
```



## EnableUIoTCoreDevice

启用设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=EnableUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN=h6phdnkjvr90iq6l
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "EnableUIoTCoreDeviceResponse"
}
```




## DisableUIoTCoreDevice

禁用设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=DisableUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN=h6phdnkjvr90iq6l
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DisableUIoTCoreDeviceResponse"
}
```




## BatchCreateUIoTCoreDevice

批量创建物联网设备，系统生成设备序列号

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)   |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceCount    | int    | 生成的设备数量                                               |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |
| DeviceSet      | array[DeviceSet] | 设备密钥列表       |  **Yes** |

### DeviceSet 设备密钥列表

| Parameter name    | Type   | Description          | Required |
| ----------------- | ------ | -------------------- | -------: |
| DeviceSN          | string | 设备序列号           |  **Yes** |
| Password          | string | 设备密码             |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=BatchCreateUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceCount=5
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchCreateUIoTCoreDeviceResponse",
    "DeviceSet": [
        {"Password:":"8jhc0phf73e885hl", "DeviceSN": "jkpoo1r6ltul7l4i"},
        {"Password:":"8jhc0phf73e886hl", "DeviceSN": "jkpoo1r6ltul7l5i"},
        {"Password:":"8jhc0phf73e887hl", "DeviceSN": "jkpoo1r6ltul7l6i"},
        {"Password:":"8jhc0phf73e888hl", "DeviceSN": "jkpoo1r6ltul7l7i"},
        {"Password:":"8jhc0phf73e889hl", "DeviceSN": "jkpoo1r6ltul7l8i"}
    ]
}
```




## BatchCreateUIoTCoreDeviceWithSN

批量创建物联网设备，用户提供设备序列号

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)   |  **Yes** |
| ProductSN      | string | 设备序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将生成的设备的名称, 可传递多值，形如: `DeviceSN.0=000`,`DeviceSN.1=111`    |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |
| DeviceSet      | array[DeviceSet] | 设备密钥列表       |  **Yes** |

### DeviceSet 设备密钥列表

| Parameter name    | Type   | Description          | Required |
| ----------------- | ------ | -------------------- | -------: |
| DeviceSN          | string | 设备序列号           |  **Yes** |
| Password          | string | 设备密码             |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=BatchCreateUIoTCoreDeviceWithSN
&ProductSN=7ab051kbfhhjakc0
&DeviceSN.0=jkpoo1r6ltul7l4i
&DeviceSN.1=jkpoo1r6ltul7l5i
&DeviceSN.2=jkpoo1r6ltul7l6i
&DeviceSN.3=jkpoo1r6ltul7l7i
&DeviceSN.4=jkpoo1r6ltul7l8i
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchCreateUIoTCoreDeviceWithSNResponse",
    "DeviceSet": [
        {"Password:":"8jhc0phf73e885hl", "DeviceSN": "jkpoo1r6ltul7l4i"},
        {"Password:":"8jhc0phf73e886hl", "DeviceSN": "jkpoo1r6ltul7l5i"},
        {"Password:":"8jhc0phf73e887hl", "DeviceSN": "jkpoo1r6ltul7l6i"},
        {"Password:":"8jhc0phf73e888hl", "DeviceSN": "jkpoo1r6ltul7l7i"},
        {"Password:":"8jhc0phf73e889hl", "DeviceSN": "jkpoo1r6ltul7l8i"}
    ]
}
```




## BatchDeleteUIoTCoreDevice

批量删除设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)   |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将删除的设备的名称, 可传递多值，形如: `DeviceSN.0=000`,`DeviceSN.1=111`   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=BatchDeleteUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN.0=jkpoo1r6ltul7l4i
&DeviceSN.1=jkpoo1r6ltul7l5i
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchDeleteUIoTCoreDeviceResponse"
}
```




## BatchEnableUIoTCoreDevice

批量启用设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将启用的设备的名称, 可传递多值，形如: `DeviceSN.0=000`,`DeviceSN.1=111`   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=BatchEnableUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN.0=jkpoo1r6ltul7l4i
&DeviceSN.1=jkpoo1r6ltul7l5i
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchEnableUIoTCoreDeviceResponse"
}
```




## BatchDisableUIoTCoreDevice

批量禁用设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)   |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将禁用的设备的名称, 可传递多值，形如: `DeviceSN.0=000`,`DeviceSN.1=111`   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=BatchDisableUIoTCoreDevice
&ProductSN=7ab051kbfhhjakc0
&DeviceSN.0=jkpoo1r6ltul7l4i
&DeviceSN.1=jkpoo1r6ltul7l5i
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchDisableUIoTCoreDeviceResponse"
}
```


# ResetUIoTCoreDevice

重置设备激活状态

# 请求参数
|Parameter name|Type|Description|Required|
|---|---|---|---|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist) |**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|ResetPassword|bool|是否重置密码,默认为否|No|

# 响应参数
|Parameter name|Type|Description|Required|
|---|---|---|---|
|RetCode|int|返回码|**Yes**|
|Action|string|操作名称|**Yes**|

# 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=ResetUIoTCoreDevice
&Region=cn-sh2
&ProductSN=7ab051kbfhhjakc0
&DeviceSN=jkpoo1r6ltul7l4i
&ResetPassword=true
```

# 响应示例
```
{
    "Action": "ResetUIoTCoreDeviceResponse", 
    "RetCode": 0
}
```



## GetUIoTCoreDeviceList

获取单个或批量设备状态、设备详情、设备列表等

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备SN，如提供则按照当前字段模糊查询                         |       No |
| Offset         | int    | 列表起始位置偏移量，默认为0                                  |       No |
| Limit          | int    | 返回最大数据长度，默认为20，最大为100                        |       No |
| ExactDeviceSN  | string | 设备SN，用于精确查询，如果提供了此字段，则DeviceSN无效            |       No |
| Status.n       | string | 设备激活状态，用于结果筛选出对应状态的设备；<br>状态枚举包括：`disabled`, `inactivated`, `offline`,`online`；<br>可以传递多值，形如：`Status.0=disabled`,`Status.1=offline`|       No |
| UpdateStatus.n | string | 设备升级状态，用于筛选对应升级状态的设备；<br>升级状态枚举包括：`unreported`,`init_version`,`to_be_updated`,<br>`updating,success`,`fail`；<br>可以传递多值，形如：`UpdateStatus.0=unreported`,`UpdateStatus.1=init_version` |       No |
|FirmwareVersion.n|string|当前固件版本，用于筛选对应版本的设备|No|
|DestVersion.n|string|目标版本，用于筛选对应版本的设备|No|

### 响应参数
| Parameter name         | Type             | Description    | Required |
| ---------------------- | ---------------- | -------------- | -------: |
| RetCode                | int              | 操作返回码     |  **Yes** |
| Action                 | string           | 操作名称       |  **Yes** |
| TotalCount             | int              | 总记录数       |  **Yes** |
| InactivatedDeviceCount | int              | 未激活设备总数 |  **Yes** |
| DeviceSet              | array[DeviceSet] | 设备列表       |  **Yes** |
| OnlineDeviceCount      | int              | 在线设备总数   |       No |

### DeviceSet 设备列表

| Parameter name    | Type   | Description          | Required |
| ----------------- | ------ | -------------------- | -------: |
|DeviceSN|string|设备序列号|**Yes**|
|Password|string|设备密码|**Yes**|
|Status|string|设备状态|**Yes**|
|CreateTime|int|创建时间|**Yes**|
|UpdateStatus|string|设备升级状态|**Yes**|
|IPAddr|string|设备ip地址|No|
|ActiveTime|int|设备激活时间|No|
|LatestOnlineTime|int|最近一次上线时间|No|
|LatestOfflineTime|int|最近一次下线时间|No|
|Description|string|设备描述|No|
|FirmwareVersion|string|设备当前固件版本|No|
|DestVersion|string|目标固件版本|No|
|ErrMsg|string|错误信息|No|
|LatestUpdateTime|string|最近一次固件更新时间|No|
|ProductSN|string|所属产品序列号|No|
|DeviceType|string|设备类型|No|
|SubDeviceNum|int|子设备数量|No|
|RemoteSSHOpen|bool|远程SSH开关是否打开|No|
|RemoteSSHPort|int|远程SSH端口|No|

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreDeviceList
&ProductSN=7ab051kbfhhjakc0
&Offset=4
&Limit=1
&DeviceSN=jkpoo1
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "TotalCount": 50,
    "InactivatedDeviceCount": 9,
    "DeviceSet": [
        {
            "DeviceSN": "jkpoo1r6ltul7l5i",
            "Password": "8jhc0phf73e885hl",
            "Status": "online",
            "CreateTime": 1564540515,
            "LatestOnlineTime": 1564540515,
            "LatestOfflineTime": 1534540515,
            "Description": "light1"
        }
    ],
    "RetCode": 0,
    "Action": "GetUIoTCoreDeviceListResponse",
    "OnlindeDeviceCount": 3
}
```



## GetUIoTCoreInactivatedDevicePasswordFile

获取未激活设备的密码文件

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreInactivatedDevicePasswordFile
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "GetUIoTCoreInactivatedDevicePasswordFileResponse"
}
```