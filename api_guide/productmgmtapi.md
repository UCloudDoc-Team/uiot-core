# 产品管理



## CreateUIoTCoreProduct

创建物联网产品

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductName    | string | 产品名称                                                     |  **Yes** |
| Description    | string | 产品描述                                                     |       No |
|NodeType|string|节点类型，分为“device”和“gateway”，默认为“device”|No|
|Gateway|bool|是否接入网关，默认为false|No|


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |
| ProductSN      | string | 产品序列号    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=CreateUIoTCoreProduct
&ProductName=电灯
&Description=电灯
&Region=cn-sh2
&NodeType=device
&Gateway=false
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "CreateUIoTCoreProductResponse"
    "ProductSN": "7ab051kbfhhjakc0"
}
```



## GetUIoTCoreProductInfo

获取产品信息

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)   |  **Yes** |
|ProductSN|string|产品序列号（如不填则使用ProductName）|No|
|ProductName|string|产品名称（如不填则使用ProductSN）|No|


### 响应参数
| Parameter name        | Type   | Description                    | Required |
| --------------------- | ------ | ------------------------------ | -------- |
| RetCode               | int    | 返回码                         | **Yes**  |
| Action                | string | 操作名称                       | **Yes**  |
| ProductSN             | string | 产品序列号                     | **Yes**  |
| ProductName           | string | 产品名称                       | **Yes**  |
| Description           | string | 产品描述                       | **Yes**  |
| DeviceNumber          | int    | 产品下设备的个数               | **Yes**  |
| CreateTime            | int    | 创建时间                       | **Yes**  |
| DynamicRegister       | string | 是否开启动态注册(on/off)       | No       |
| PreRegister           | string | 是否开启预注册(on/off)         | No       |
| DeviceShadow          | string | 是否开启设备影子(on/off)       | No       |
| Password              | string | 产品密钥                       | No       |
| IsPublish             | bool   | 产品是否发布                   | No       |
| ActivatedDeviceNumber | int    | 产品下已激活的设备数量         | No       |
| OnlineDeviceNumber    | int    | 产品下在线设备数               | No       |
| NodeType              | string | 节点类型，“device"或 "gateway" | No       |
| Gateway               | bool   | 是否接入网关                   | No       |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreProductInfo
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&ProductName=productname
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "NodeType": "device",
    "PreRegister": "on", 
    "Action": "GetUIoTCoreProductInfoResponse",
    "ProductSN": "7ab051kbfhhjakc0",
    "ProductName": "电灯",
    "Description": "电灯",
    "DeviceNumber": 100,
    "CreateTime": 1564541035,
    "Gateway": false, 
    "DynamicRegister": "off",
    "DeviceShadow": "on",
    "Password": "8jhc0phf73e887hl",
    "IsPublish": false,
    "ActivatedDeviceNumber": 7,
    "OnlineDeviceNumber":10
}
```



## ModifyUIoTCoreProduct

修改物联网产品

### 请求参数
| Parameter name | Type   | Description                                                  | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------: |
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
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
https://api-cn-sh2.iot.ucloud.cn/?Action=ModifyUIoTCoreProduct
&ProductSN=7ab051kbfhhjakc0
&ProductName=light
&Description=light
&Region=cn-sh2
&公共请求参数
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
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序号                                                     |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=DeleteUIoTCoreProduct
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&公共请求参数
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
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
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

|Parameter name|Type|Description|Required|
|---|---|---|---|
|ProductSN|string|产品序列号|**Yes**|
|ProductName|string|产品名称|**Yes**|
|CreateTime|int|产品创建时间|**Yes**|
|DynamicRegister|string|是否开启动态注册(on/off)|**Yes**|
|PreRegister|string|是否开启预注册(on/off)|**Yes**|
|DeviceShadow|string|是否开启动态注册(on/off)|**Yes**|
|Password|string|产品密钥|**Yes**|
|IsPublish|bool|产品是否发布|**Yes**|
|Description|string|产品描述|**Yes**|
|DeviceNumber|int|产品下的设备数量|**Yes**|
|ActivatedDeviceNumber|int|产品下已激活的设备数量|**Yes**|
|OnlineDeviceNumber|int|产品下在线设备数|**Yes**|
|NodeType|string|产品类型。“device”或“gateway"|No|
|Gateway|bool|是否接入网关|No|

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreProductList
&Offset=0
&Limit=1
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "TotalCount": 9,
    "ProductSet": [
        {
            "ProductSN": "7ab051kbfhhjakc0",
            "ProductName": "light",
            "Description": "light",
            "DeviceNumber": 100,
            "CreateTime": 1564541035,
            "DynamicRegister": "off",
            "PreRegister": false,
            "DeviceShadow": "on",
            "Password": "8jhc0phf73e887hl",
            "IsPublish": false,
            "ActivatedDeviceNumber": 7,
            "OnlineDeviceNumber":10,
            "NodeType":"device",
            "Gateway":false
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
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=EnableUIoTCoreDynamicRegister
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&公共请求参数
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
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)  |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=DisableUIoTCoreDynamicRegister
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&公共请求参数
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
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)   |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

### 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=PublishUIoTCoreProduct
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&公共请求参数
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
| Region         | string | 地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)   |  **Yes** |
| ProductSN      | string | 产品序列号                                                   |  **Yes** |


### 响应参数
| Parameter name | Type   | Description | Required |
| -------------- | ------ | ----------- | -------: |
| RetCode        | int    | 操作返回码  |  **Yes** |
| Action         | string | 操作名称    |  **Yes** |

## 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=UnpublishUIoTCoreProduct
&ProductSN=7ab051kbfhhjakc0
&Region=cn-sh2
&公共请求参数
```
### 响应示例
```
{
    "RetCode": 0,
    "Action": "UnpublishUIoTCoreProductResponse"
}
```