{{indexmenu_n>1}}

# 产品管理



## CreateUIoTCoreProduct

创建物联网产品

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductName    | string | 产品名称                                                     |  **Yes** |
| Description    | string | 产品描述                                                     |       No |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=CreateUIoTCoreProduct
&ProductName=QmHPudWV
&Description=plNlsSmv
&ProjectId=npbnwhnb
&Region=UQxqYeOi
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreProductResponse"
}
```



## GetUIoTCoreProductInfo

获取产品信息

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |


### 响应参数
| Parameter name        | Type   | Description              | Required |
| --------------------- | ------ | ------------------------ | -------: |
| RetCode               | int    | 操作返回码               |  **Yes** |
| Action                | string | 操作名称                 |  **Yes** |
| ProductSN             | string | 产品序列号               |  **Yes** |
| ProductName           | string | 产品名称                 |  **Yes** |
| Description           | string | 产品描述                 |  **Yes** |
| DeviceNumber          | int    | 产品下设备的个数         |  **Yes** |
| CreateTime            | int    | 创建时间                 |  **Yes** |
| DynamicRegister       | string | 是否开启动态注册(on/off) |       No |
| DeviceShadow          | string | 是否开启设备影子(on/off) |       No |
| Password              | string | 产品密钥                 |       No |
| IsPublish             | bool   | 产品是否发布             |       No |
| FirmwareNumber        | int    | 产品下的固件数量         |       No |
| ActivatedDeviceNumber | int    | 产品下已激活的设备数量   |       No |

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreProductInfo
&ProjectId=zsBblvuu
&ProductSN=rxKrUpAX
&Region=pMoXonyh
```
### 响应示例
```
{
    "ProductSN": "gjDkEPgK",
    "ProductName": "qMYdiIAC",
    "Description": "EcoDIWBI",
    "DeviceNumber": 2,
    "CreateTime": 2,
    "RetCode": 0,
    "Action": "GetUIoTCoreProductInfoResponse",
    "DynamicRegister": "tNUXiClO",
    "DeviceShadow": "CJRMalKZ",
    "Password": "mpsEWflR",
    "IsPublish": false,
    "FirmwareNumber": 6,
    "ActivatedDeviceNumber": 7
}
```



## ModifyUIoTCoreProduct

修改物联网产品

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |
| ProductName    | string | 修改后的产品名称                                             |       No |
| Description    | string | 修改后的产品描述                                             |       No |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=ModifyUIoTCoreProduct
&ProductSN=dApNJjnD
&ProductName=UeOtOcGY
&Description=HmzADyLU
&ProjectId=jAEVkWfw
&Region=pjfRsejV
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "ModifyUIoTCoreProductResponse"
}
```



## DeleteUIoTCoreProduct

删除物联网产品

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品序号                                                     |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=DeleteUIoTCoreProduct
&ProductSN=RCpKeRbj
&ProjectId=aMKHrxpV
&ProjectId=MjysljKm
&Region=zfQjHRyA
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DeleteUIoTCoreProductResponse"
}
```



## GetUIoTCoreProductList

获取产品信息列表

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](../summary/regionlist.html)   |  **Yes** |
| ProjectId      | string | 项目ID。不填写为默认项目，子帐号必须填写。 请参考[GetProjectList接口](../summary/get_project_list.html) |       No |
| ProductSN      | string | 产品SN，如果提供则根据此字段模糊查找                         |       No |
| ProductName    | string | 产品名称，如果提供则根据此字段模糊查找                       |       No |
| Offset         | int    | 列表起始位置偏移量，默认为0                                  |       No |
| Limit          | int    | 返回最大数据长度，默认为20，最大为100                        |       No |


### 响应参数
| Parameter name | Type              | Description  | Required |
| -------------- | ----------------- | ------------ | -------: |
| RetCode        | int               | 操作返回码   |  **Yes** |
| Action         | string            | 操作名称     |  **Yes** |
| TotalCount     | int               | 总记录数     |  **Yes** |
| ProductSet     | array[ProductSet] | 产品列表信息 |  **Yes** |

### ProductSet 产品列表

| Parameter name        | Type   | Description              | Required |
| --------------------- | ------ | ------------------------ | -------: |
| ProductSN             | string | 产品序列号               |  **Yes** |
| ProductName           | string | 产品名称                 |  **Yes** |
| CreateTime            | int    | 产品创建时间             |  **Yes** |
| DynamicRegister       | string | 是否开启动态注册(on/off) |  **Yes** |
| DeviceShadow          | string | 是否开启动态注册(on/off) |  **Yes** |
| Password              | string | 产品密钥                 |  **Yes** |
| IsPublish             | bool   | 产品是否发布             |  **Yes** |
| Description           | string | 产品描述                 |  **Yes** |
| DeviceNumber          | int    | 产品下的设备数量         |  **Yes** |
| FirmwareNumber        | int    | 产品下的固件数量         |  **Yes** |
| ActivatedDeviceNumber | int    | 产品下已激活的设备数量   |  **Yes** |

### 请求示例
```
https://api.ucloud.cn/?Action=GetUIoTCoreProductList
&Offset=6
&Limit=10050
&ProjectId=yqPCQMKy
&ProductSN=jVEzJKmo
&ProductName=gfHOodRZ
&Region=LlfmYuzA
```
### 响应示例
```
{
    "TotalCount": 9,
    "ProductSet": [
        {
            "ProductSN": "UbSggzPd",
            "ProductName": "vdEqTZFw",
            "CreateTime": 7,
            "Description": "vobWGoum",
            "DeviceNumber": 9
        },
        {
            "ProductSN": "yDHlJXBU",
            "ProductName": "YKpzWxAm",
            "CreateTime": 6,
            "Description": "KTAcCMzl",
            "DeviceNumber": 4
        }
    ],
    "RetCode": 0,
    "Action": "GetUIoTCoreProductListResponse"
}
```



## EnableUIoTCoreDynamicRegister

打开设备动态注册功能

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
https://api.ucloud.cn/?Action=EnableUIoTCoreDynamicRegister
&Region=cn-zj
&ProjectId=aObJFQLG
&ProductSN=FGUpVeZH
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "EnableUIoTCoreDynamicRegisterResponse"
}
```



## DisableUIoTCoreDynamicRegister

禁用产品下设备动态注册

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
https://api.ucloud.cn/?Action=DisableUIoTCoreDynamicRegister
&Region=cn-zj
&ProjectId=groYGqwB
&ProductSN=WfPBywAd
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "DisableUIoTCoreDynamicRegisterResponse"
}
```



## PublishUIoTCoreProduct

发布产品

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
https://api.ucloud.cn/?Action=PublishUIoTCoreProduct
&Region=cn-zj
&ProjectId=UpRqzvsw
&ProductSN=SEfgZuMU
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "PublishUIoTCoreProductResponse"
}
```




## UnpublishUIoTCoreProduct

撤销发布产品

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

## 请求示例
```
https://api.ucloud.cn/?Action=UnpublishUIoTCoreProduct
&Region=cn-zj
&ProjectId=VoqSzaxg
&ProductSN=oOVURiCv
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "UnpublishUIoTCoreProductResponse"
}
```