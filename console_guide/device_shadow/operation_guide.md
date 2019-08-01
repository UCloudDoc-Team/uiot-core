{{indexmenu_n>2}}

# 设备影子相关操作

对设备影子的操作包括：

- 设备端获取设备影子文档；

- 设备端上报状态更新设备影子；

- 设备端删除设备影子属性；

- 设备端重置设备影子版本；

- 应用服务端更新设备影子期望值，对设备进行属性设置；

- 应用服务端获取设备影子状态；

- 应用服务端关闭/开启设备影子；



设备影子版本号的相关说明：

- 设备影子每次更新，无论是云端应用服务还是设备端，都会发生版本的增加，每次+1；

- 设备影子的版本号由平台维护，设备端也可以重置设备影子版本；

- 设备更新属性的版本号必须和平台的设备影子的版本号一致才能成功上报，否则平台会下发**control**信息，并跟随平台设备影子的版本号；

- 设备影子的版本号为32位整型（**int32**），设备端需要维护好，特别是发生溢出翻转时；

- 每当设备影子发生版本更新时，平台会自动往**/$system/${ProductSN}/${DeviceSN}/shadow/document**发送完整的设备影子文档，供规则引擎使用；



## 设备影子涉及的Topic

|Topic | 权限|描述|
|---|---|---|
| /$system/${ProductSN}/${DeviceSN}/shadow/upstream |发布|上行操作设备影子（更新、删除）|
|/$system/${ProductSN}/${DeviceSN}/shadow/downstream | 订阅| 设置期望值|
|/$system/${ProductSN}/${DeviceSN}/shadow/get|发布|获取设备影子|
|/$system/${ProductSN}/${DeviceSN}/shadow/get_reply|订阅|获取设备影子返回|
|/$system/${ProductSN}/${DeviceSN}/shadow/document|-|设备影子发生变化时将发送完整的设备影子文档(仅用于规则引擎)|



## 应用用例
假设设备拥有**temperature**和**humidity**两个属性，云端应用可以发送期望温度值给设备端。



### 设备端获取设备影子文档

设备可以主动获取平台上缓存的当前设备影子文档。

1\. 设备发送任意内容到获取设备影子Topic

```
Publish Topic /$system/${ProductSN}/${DeviceSN}/shadow/get

{
  "Method": "get"
}
```

2\. 设备订阅返回设备影子文档Topic，返回的是一个设备影子全量值，包括设备属性、期望值、版本号。

```
Subscribe Topic /$system/${ProductSN}/${DeviceSN}/shadow/get_reply

{
  "State": {
    "Reported": {},
    "Desired": {}
  },
  "Metadata": {
    "Reported": {},
    "Desired": {}
  },
  "Timestamp": 1562904212,
  "Version": 0
}
```



### 设备端更新设备影子状态

1\. 参考[设备端获取设备影子文档](#设备端获取设备影子文档)获取设备影子版本号，使用**update**方法，上报属性值。只有上报版本号和平台设备影子版本号一致才能更新，否则会出现版本冲突。

```
    Publish Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream
    
    {
      "Method": "update",
      "State": {
        "Reported": {
          "temperature": 26,
          "humidity": 57
        }
      },
      "Version": 0
    }
```

2\. 平台会返回更新成功，同时版本号会增1。

```
    Subscribe Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream
    
    {
      "Method": "reply",
      "Payload": {
        "RetCode": 0
      },
      "Version": 1,
      "Timestamp": 1562909435
    }
```

3\. 平台端设备影子更新为：

```
    {
      "State": {
        "Reported": {
          "temperature": 26,
          "humidity": 57
        },
        "Desired": {}
      },
      "Metadata": {
        "Reported": {
          "temperature": {
            "Timestamp": 1562909435
          }
          "humidity": {
            "Timestamp": 1562909435
          }
        },
        "Desired": {}
      },
      "Timestamp": 1562909435,
      "Version": 2
    }
```

4\. 设备需要维护好该版本号，否则会发生版本冲突。发生冲突时，平台返回全量设备影子**control**信息，**Retcode**为**100026**表示版本冲突，设备需要根据当前情况对其中内容做调整，设备端需要重新对齐版本号**Version**。

```
    Subscribe Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream
    
    {
      "Method": "control",
      "Payload": {
        "RetCode": 100026,
        "State": {
          "Reported": {
            "humidity": 57,
            "temperature": 26
          },
          "Desired": {}
        },
        "Metadata": {
          "Reported": {
            "humidity": {
              "Timestamp": 1562909435
            },
            "temperature": {
              "Timestamp": 1562909435
            }
          },
          "Desired": {}
        }
      },
      "Version": 1,
      "Timestamp": 1562909688
    }
```

|参数|说明|
|---|---|
|Method|表示对设备影子的操作类型，包括update更新/control控制/ reply回复|
|Retcode|响应码，具体可以参考下面的响应码|

|响应码|说明|
|---|---|
|0 |请求成功|
|230 |不正确的JSON格式|
|230 |消息体缺少 method 信息|
|230 |消息体缺少 state 字段|
|230 |消息体 version 不是数字|
|230 |消息体缺少 desired 字段|
|230 |消息体 method 是无效的方法|
|100026 |影子文档与消息体 version 版本冲突，顺便返回version的值|
|130 |设备影子服务端处理异常|
    


### 设备端删除设备影子属性

1\.  参考[设备端获取设备影子文档](#设备端获取设备影子文档)获取设备影子版本号，使用**delete**方法，删除属性。
只有上报数据版本号和平台设备影子版本号一致才能删除，否则会出现版本冲突。

- 删除某一属性

```
    Publish Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream"
    
    {
      "Method": "delete",
      "State": {
        "Reported": {
          "temperature": null
        }
      },
      "version": 1
    }
```

- 删除全部属性

```
    Publish Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream"
    
    {
      "Method": "delete",
      "State": {
        "Reported": null
      },
      "version": 1
    }
```

2\. 平台会返回删除成功，同时版本号会增1。

```
    Subscribe Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream
    
    {
      "Method": "reply",
      "Payload": {
        "RetCode": 0
      },
      "Version": 2,
      "Timestamp": 1562911255
    }
```

3\. 平台端设备影子更新为：

```
    {
      "State": {
        "Reported": {
          "humidity": 57
        },
        "Desired": {}
      },
      "Metadata": {
        "Reported": {
          "humidity": {
            "Timestamp": 1562909435
          }
        },
        "Desired": {}
      },
      "Timestamp": 1562911400,
      "Version": 2
    }
```

4\. 设备需要维护好该版本号，否则会发生版本冲突。发生冲突时，平台返回全量设备影子**control**信息，**Retcode**为**100026**表示版本冲突，设备需要根据当前情况对其中内容做调整，设备端需要重新对齐版本号**Version**。



### 设备重置设备影子版本

当设备发送的**update**请求中的**Version**为特殊值**-1**，设备影子会将影子文档版本更新为**0**，同时清空（如有）**Desired**中的值。清空设备影子版本，不影响设备属性的正常上报。

1\. 上报属性，并使用**Version**为**-1**。

```
    Publish Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream
    
    {
      "Method": "update",
      "State": {
        "Reported": {
          "temperature": 26,
          "humidity": 57
        }
      },
      "Version": -1
    }
```

2\. 平台会返回重置成功，同时版本号重置为0。

```
    Subscribe Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream
    
    {
      "Method": "reply",
      "Payload": {
        "RetCode": 0
      },
      "Version": 0,
      "Timestamp": 1562912657
    }
```

3\. 平台端设备影子更新为：

```
    {
      "State": {
        "Reported": {
          "humidity": 57,
          "temperature": 26
        },
        "Desired": {}
      },
      "Metadata": {
        "Reported": {
          "humidity": {
            "Timestamp": 1562912657
          },
          "temperature": {
            "Timestamp": 1562912657
          }
        },
        "Desired": {}
      },
      "Timestamp": 1562912800,
      "Version": 0
    }
```



### 设备影子更新时转发到规则引擎

设备影子更新时，平台将完整设备影子文档发到 **/$system/${ProductSN}/${DeviceSN}/shadow/document** ，通过规则引擎可流转到平台以外的云产品，比如UHost、UDB、UKafka等。该Topic仅用于规则引擎流转，设备端不能发布或订阅。



### 应用程序更新设备影子期望值

1\. 应用服务端通过[UpdateUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)，下发需要发给设备端的期望值。  
UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[关于API接入](../../api_guide/api_guidehelp)，其他参数参考[UpdateUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)

```
    POST  HTTP/1.1
    Host: api.ucloud.cn
    Content-Type: application/json
    Body:
    {
      "Action": "UpdateUIoTCoreDeviceShadow",
      "ProductSN": "70ly1tvowt696r15",
      "DeviceSN":"00:14:32:e1:72:f1",
      "Desired": "eyJ0ZW1wZXJhdHVyZSI6MTd9", //base64Encode({"temperature":17})
      "ShadowVersion": 1,
      "ProjectId": "org-z44lmf12e",
      "PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
      "Region": "cn-sh2",
      "Signature": "dwe6b4e35df41b42232e059f6020r7fd51b2889e"
    }
```

2\. 平台更新设备影子并添加**Desired**键值，版本号加1，并通过**/$system/${ProductSN}/${DeviceSN}/shadow/downstream**下发给设备，假如设备在线的话会立即收到，如果设备不在线需要设备上线后主动获取一次设备影子文档，参考[设备端获取设备影子文档](#设备端获取设备影子文档)。

```
    Subscribe Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream
    
    {
      "Method": "control",
      "Payload": {
        "RetCode": 0,
        "State": {
          "Desired": {
            "temperature": 17
          }
        },
        "Metadata": {
          "Desired": {
            "temperature": {
              "Timestamp": 1562917500
            }
          }
        }
      },
      "Version": 2,
      "Timestamp": 1562917504
    }
```

3\. 平台端设备影子更新为：

```
    {
      "State": {
        "Reported": {
          "humidity": 57,
          "temperature": 26
        },
        "Desired": {
          "temperature": 17
        }
      },
      "Metadata": {
        "Reported": {
          "humidity": {
            "Timestamp": 1562912843
          },
          "temperature": {
            "Timestamp": 1562912843
          }
        },
        "Desired": {
          "temperature": {
            "Timestamp": 1562917500
          }
        }
      },
      "Timestamp": 1562917600,
      "Version": 2
    }
```

4\. 在线设备收到带有期望值的**control**消息之后，将自身状态值设为期望值（本例中的温度一般是控制恒温加热器）。

5\. 设备端状态修改后，需要将设备影子的**Desired**键置空。

```
    Publish Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream"
    
    {
      "Method": "update",
      "State": {
        "Desired": null
      },
      "Version": 2
    }
```

6\. 平台会更新设备影子文档，清除设备影子**State**和**Metadata**中的**Desired**字段，将Reported中的该字段设置成**Desired**的值（如果Desired置空的同时，Reported该属性为另外的值，则记录上报的Reported值），同时版本号增1，此时设备影子文档更新为

```
    {
      "State": {
        "Reported": {
          "humidity": 57,
          "temperature": 17
        },
        "Desired": {}
      },
      "Metadata": {
        "Reported": {
          "humidity": {
            "Timestamp": 1562912843
          },
          "temperature": {
            "Timestamp": 1562919549
          }
        },
        "Desired": {}
      },
      "Timestamp": 1562919600,
      "Version": 3
    }
```

7\. 平台会下发置空成功消息给设备

```
    {
      "Method": "reply",
      "Payload": {
        "RetCode": 0
      },
      "Version": 3,
      "Timestamp": 1562919549
    }
```



### 应用程序获取设备影子状态

应用程序直接通过[GetUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)可以获取设备影子状态。  
UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[关于API接入](../../api_guide/api_guidehelp)，其他参数参考[GetUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)

```
POST  HTTP/1.1
Host: api.ucloud.cn
Content-Type: application/json
Body:
{
  "Action": "UpdateUIoTCoreDeviceShadow",
  "ProductSN": "70ly1tvowt696r15",
  "DeviceSN":"00:14:32:e1:72:f1
",
  "ProjectId": "org-z44lmf12e",
  "PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
  "Region": "cn-sh2",
  "Signature": "ewe6b4e35de41b42232e059f6020r7fd51b2889e"
}
```



### 应用程序开启/关闭设备影子

应用程序直接通过[EnableUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)和[DisableUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)可以开启/关闭设备影子状态。  
UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[关于API接入](../../api_guide/api_guidehelp)，其他参数参考[EnableUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)和[DisableUIoTCoreDeviceShadow](../../api_guide/deviceshadowmgmtapi)。

```
POST  HTTP/1.1
Host: api.ucloud.cn
Content-Type: application/json
Body:
{
  "Action": "EnableUIoTCoreDeviceShadow", //关闭为：DisableUIoTCoreDeviceShadow
  "ProductSN": "70ly1tvowt696r15",
  "ProjectId": "org-z44lmf12e",
  "PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
  "Region": "cn-sh2",
  "Signature": "ewe6b4e35de41b42232e059f6020r7fd51b2889e"
}
```
