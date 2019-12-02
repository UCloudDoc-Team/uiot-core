# 上传文件

## QueryUIoTCoreDeviceFileList

查询设备上传的文件列表

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist) | **Yes** |
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|No|
|FileName|string|文件名称|No|
|Offset|int|列表起始位置偏移量，默认为0|No|
|Limit|int|返回最大数据长度，默认为20，最大为100|No|
|URLExpire|int|下载URL的过期时间，单位秒。小于等于0值则有效期为60年，默认为0|No|

### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|FileList|array[FileInfo]|文件列表|**Yes**|
|TotalCount|int|文件总数|No|

#### FileInfo

文件信息

|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|FileName|string|文件名称|**Yes**|
|FileSize|int|文件大小|**Yes**|
|CreateTime|int|创建时间|**Yes**|
|URL|string|文件下载链接|**Yes**|

### 请求示例

```
https://api-cn-sh2.iot.ucloud.cn/?Action=QueryUIoTCoreDeviceFileList
&Region=cn-sh2
&ProductSN=s488594zqqrz7v3y
&DeviceSN=10001
&Offset=0
&Limit=9
```

### 响应示例
```
{
    "Action": "QueryUIoTCoreDeviceFileListResponse",
    "RetCode": 0,
    "FileList": [
        {
            "FileName": "umrLuNQz",
            "CreateTime": 1248577,
            "FileSize": 124,
            "URL":"http://uiotcore-55977352-55738012.cn-sh2.ufileos.com/s488594zqqrz7v3y/vfvjqYKWIdHbK/filename.txt?Expires=1575028870&Signature=FDtXmo%3D&UCloudPublicKey=dhXd%2F0B6EckE%2BCZ%2FFI%3D"
        }
    ],
    "TotalCount": 7
}
```

# QueryUIoTCoreDeviceFile

获取设备文件信息

# 请求参数
|Parameter name|Type|Description|Required|
|---|---|---|---|
|Region|string|地地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)|**Yes**|
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|FileName|string|文件名称，文件名称不能以`/`结尾|**Yes**|
|URLExpire|int|下载URL的过期时间，单位秒。小于等于0值则有效期为60年，默认为0|No|

# 响应参数
|Parameter name|Type|Description|Required|
|---|---|---|---|
|RetCode|int|返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|FileInfo|object|文件信息|**Yes**|

## FileInfo
|Parameter name|Type|Description|Required|
|---|---|---|---|
|FileName|string|文件名称|**Yes**|
|FileSize|int|文件大小|**Yes**|
|CreateTime|int|创建时间|**Yes**|
|URL|string|文件下载链接|**Yes**|

# 请求示例
```
https://api-cn-sh2.iot.ucloud.cn/?Action=QueryUIoTCoreDeviceFile
&Region=cn-zj
&ProductSN=s488594zqqrz7v3y
&DeviceSN=vfvjqYKWIdHbK
&FileName=filename.txt
&URLExpire=0
```

# 响应示例
```
{
    "Action": "QueryUIoTCoreDeviceFileResponse", 
    "FileInfo": {
            "FileName": "umrLuNQz",
            "CreateTime": 1248577,
            "FileSize": 124,
            "URL":"http://uiotcore-55977352-55738012.cn-sh2.ufileos.com/s488594zqqrz7v3y/vfvjqYKWIdHbK/filename.txt?Expires=1575028870&Signature=FDtXmo%3D&UCloudPublicKey=dhXd%2F0B6EckE%2BCZ%2FFI%3D"		
        }, 
    "RetCode": 0
}
```


## GetUIoTCoreDeviceFileURL

获取设备文件的下载链接，有效期30分钟

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist) | **Yes** |
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|FileName|string|文件名称，文件名称不能以 / 结尾|**Yes**|
|URLExpire|int|下载URL的过期时间，单位秒。小于等于0值则有效期为60年，默认为0|No|

### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|
|URL|string|下载链接|**Yes**|

### 请求示例

```
https://api-cn-sh2.iot.ucloud.cn/?Action=GetUIoTCoreDeviceFileURL
&Region=cn-sh2
&ProductSN=s488594zqqrz7v3y
&DeviceSN=10001
&FileName=ota.zip
```

### 响应示例

```
{
    "RetCode": 0,
    "Action": "GetUIoTCoreDeviceFileURLResponse",
    "URL": "url"
}
```

## DeleteUIoTCoreDeviceFile

删除设备文件

### 请求参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|Region|string|地域。 参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist) | **Yes** |
|ProductSN|string|产品序列号|**Yes**|
|DeviceSN|string|设备序列号|**Yes**|
|FileName|string|文件名称，文件名称不能以 / 结尾|**Yes**|


### 响应参数
|Parameter name|Type|Description|Required|
|------|------|--------|----:|
|RetCode|int|操作返回码|**Yes**|
|Action|string|操作名称|**Yes**|

### 请求示例

```
https://api-cn-sh2.iot.ucloud.cn/?Action=DeleteUIoTCoreDeviceFile
&Region=cn-sh2
&ProductSN=s488594zqqrz7v3y
&DeviceSN=10001
&FileName=ota.ziq

```

### 响应示例

```
{
    "RetCode": 0,
    "Action": "DeleteUIoTCoreDeviceFileResponse"
}
```
