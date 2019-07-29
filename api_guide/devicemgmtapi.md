{{indexmenu_n>5}}

# 设备管理



## CreateUIoTCoreDevice

创建物联网设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号，不填则由系统自动生成                             |       No |
| Description    | string | 设备描述信息                                                 |       No |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |
| Password       | string | 设备密钥    |       No |

### 请求示例
```
https://api.ucloud.cn/?Action=CreateUIoTCoreDevice
&ProductSN=lOIysDWJ
&DeviceSN=vGRfkKcd
&Description=NbMdzhUI
&ProjectId=qUckfKHd
&Region=MrfhKJZs
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreDeviceResponse",
    "DevicePassword": "OjbZLcqf"
}
```



## ModifyUIoTCoreDevice

修改物联网设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
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
https://api.ucloud.cn/?Action=ModifyUIoTCoreDevice
&ProductSN=ooLvUroq
&DeviceSN=hqfDsbCH
&NewDescription=HZKrOzQw
&ProjectId=ImvaimaE
&Region=jTUxmpjV
&Region=FVFZEZIy
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
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=DeleteUIoTCoreDevice
&ProductSN=ZxwAVWNE
&DeviceSN=hfZYejwi
&ProjectId=tCBHHfRr
&Region=ocrolYkx
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
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=EnableUIoTCoreDevice
&ProductSN=oEraZYtN
&DeviceSN=KlXLwTCK
&ProjectId=ithdvgCm
&Region=OymiAYnB
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
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=DisableUIoTCoreDevice
&ProductSN=ksikAKhI
&DeviceSN=aDbbIIES
&ProjectId=hrOPuYxl
&Region=rrOejcMe
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
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceCount    | int    | 生成的设备数量                                               |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=BatchCreateUIoTCoreDevice
&ProductSN=NqIjuhth
&DeviceCount=500
&ProjectId=dsSArCyX
&Region=mgaKcHeL
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchCreateUIoTCoreDeviceResponse"
}
```




## BatchCreateUIoTCoreDeviceWithSN

批量创建物联网设备，用户提供设备序列号

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 设备序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将生成的设备的名称, 可数组传递多值，形如: DeviceSN.0=111   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=BatchCreateUIoTCoreDeviceWithSN
&ProductSN=VFvBpBMc
&DeviceSN.n=trQJoYlV
&ProjectId=chpzkqoA
&Region=kYaVJqCH
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchCreateUIoTCoreDeviceWithSNResponse"
}
```




## BatchDeleteUIoTCoreDevice

批量删除设备

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将删除的设备的名称, 可数组传递多值，形如: DeviceSN.0=111   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=BatchDeleteUIoTCoreDevice
&ProductSN=cUlVPIxh
&DeviceSN.n=fUGucMqn
&ProjectId=uhHYfVTs
&Region=SgoFaBKw
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
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将启用的设备的名称, 可数组传递多值，形如: DeviceSN.0=111   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=BatchEnableUIoTCoreDevice
&ProductSN=gaSmWUGm
&DeviceSN.n=SMOBqSnl
&ProjectId=LXNlIpbt
&Region=PUTOkjPY
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
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN.n     | string | 即将禁用的设备的名称, 可数组传递多值，形如: DeviceSN.0=111   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=BatchDisableUIoTCoreDevice
&ProductSN=fqFvZTlh
&DeviceSN.n=sGolWSIL
&ProjectId=wVQWJgzb
&Region=FKqvyXDW
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "BatchDisableUIoTCoreDeviceResponse"
}
```




## GetUIoTCoreDeviceList

获取设备列表

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| DeviceSN       | string | 设备SN，如提供则按照当前字段模糊查询                         |       No |
| Offset         | int    | 列表起始位置偏移量，默认为0                                  |       No |
| Limit          | int    | 返回最大数据长度，默认为20，最大为100                        |       No |


### 响应参数
| Parameter name         | Type             | Description    | Required |
| ---------------------- | ---------------- | -------------- | -------: |
| RetCode                | int              | 操作返回码     |  **Yes** |
| Action                 | string           | 操作名称       |  **Yes** |
| TotalCount             | int              | 总记录数       |  **Yes** |
| InactivatedDeviceCount | int              | 未激活设备总数 |  **Yes** |
| DeviceSet              | array[DeviceSet] | 设备列表       |  **Yes** |
| OnlindeDeviceCount     | int              | 在线设备总数   |       No |

### DeviceSet 设备列表

| Parameter name    | Type   | Description          | Required |
| ----------------- | ------ | -------------------- | -------: |
| DeviceSN          | string | 设备序列号           |  **Yes** |
| Password          | string | 设备密码             |  **Yes** |
| Status            | string | 设备状态             |  **Yes** |
| CreateTime        | int    | 创建时间             |  **Yes** |
| UpdateStatus      | string | 设备升级状态         |  **Yes** |
| ActiveTime        | int    | 设备激活时间         |       No |
| LatestOnlineTime  | int    | 最近一次上线时间     |       No |
| LatestOfflineTime | int    | 最近一次下线时间     |       No |
| Description       | string | 设备描述             |       No |
| FirmwareVersion   | string | 设备当前固件版本     |       No |
| DestVersion       | string | 目标固件版本         |       No |
| ErrMsg            | string | 错误信息             |       No |
| LatestUpdateTime  | string | 最近一次固件更新时间 |       No |

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreDeviceList
&ProductSN=IblUqWrM
&Offset=4
&Limit=50
&ProjectId=TtXVWjuG
&DeviceSN=YQIWgQro
&Region=VBXqzWMb
```
### 响应示例
```
{
    "TotalCount": 2,
    "InactivatedDeviceCount": 9,
    "DeviceSet": [
        {
            "DeviceSN": "YVqPZMHL",
            "Password": "DVsvqbzZ",
            "Status": "PqOObuEb",
            "CreateTime": 8,
            "LatestOnlineTime": 3,
            "LatestOfflineTime": 4,
            "Description": "IGZMbdmj"
        },
        {
            "DeviceSN": "oxyoXYtt",
            "Password": "ufAsSkYH",
            "Status": "rPpxTueo",
            "CreateTime": 4,
            "LatestOnlineTime": 8,
            "LatestOfflineTime": 6,
            "Description": "aJZuRaUt"
        },
        {
            "DeviceSN": "gUnseqww",
            "Password": "XTtktyXh",
            "Status": "EvnTSDPc",
            "CreateTime": 9,
            "LatestOnlineTime": 2,
            "LatestOfflineTime": 2,
            "Description": "qGkUOjZD"
        },
        {
            "DeviceSN": "wexAKsJK",
            "Password": "gPrRgGWm",
            "Status": "TNdIwXvy",
            "CreateTime": 3,
            "LatestOnlineTime": 3,
            "LatestOfflineTime": 5,
            "Description": "TyUTLMOq"
        },
        {
            "DeviceSN": "hHjIeOjW",
            "Password": "kdRYRPJk",
            "Status": "SDRurPQd",
            "CreateTime": 4,
            "LatestOnlineTime": 6,
            "LatestOfflineTime": 1,
            "Description": "vycPfkht"
        },
        {
            "DeviceSN": "XeNYIGrm",
            "Password": "beiGYlCQ",
            "Status": "tNLhJPQI",
            "CreateTime": 4,
            "LatestOnlineTime": 3,
            "LatestOfflineTime": 1,
            "Description": "fjkxQxXI"
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
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreInactivatedDevicePasswordFile
&ProductSN=ZETblNWb
&ProjectId=GzdTItXK
&Region=IxrcFmle
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "GetUIoTCoreInactivatedDevicePasswordFileResponse"
}
```