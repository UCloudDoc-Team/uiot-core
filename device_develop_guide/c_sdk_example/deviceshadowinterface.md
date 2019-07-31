{{indexmenu_n>4}}

## 如何新建一个修改设备影子文档的请求图例
注：图例中已将一个完整的更新或者删除操作拆解开讲解
![](../../images/设备影子-1.png)

## 设备影子支持的操作类型 (c-sdk\src\sdk-impl\uiot_export_shadow.h 枚举Method)
* **GET** - 获取云平台上的最新影子文档并同步属性值和版本号
* **UPDATE** - 更新云平台上的影子文档属性
* **UPDATE_AND_RESET_VER** - 更新云平台上的影子文档属性并清零版本号
* **DELETE** - 删除云平台上的影子文档属性
* **DELETE_ALL** - 删除云平台上的影子文档中的全部属性
* **REPLY_CONTROL_UPDATE** - 当版本不一致，云平台回复control后，设备根据最新影子文档更新完本地属性后回复的UPDATE消息
* **REPLY_CONTROL_DELETE** - 当版本不一致，云平台回复control后，设备根据最新影子文档更新完本地属性后回复的DELETE消息

## 设备影子支持的属性值类型 (c-sdk\src\sdk-impl\uiot_export_shadow.h)
* **int32_t** - 32位有符号整型
* **int16_t** - 16位有符号整型
* **int8_t** - 8位有符号整型
* **uint32_t** - 32位无符号整型
* **uint16_t** - 16位无符号整型
* **uint8_t** - 8位无符号整型
* **float** - 单精度浮点型
* **double** - 双精度浮点型
* **bool** - 布尔型
* **char *** - 字符串
* **char *** - JSON对象

## 设备属性回调函数说明

每个属性都要有自己的回调函数，由用户实现，主要功能是在云平台下发属性期望值时决定如何在当前值和期望值间取值，<br>
或者可以根据两个值取中间范围内的某一个值。如果回调函数中选择了云平台的期望值则不需要添加进请求向云平台上报，<br>
如果最终属性的值与云平台期望值不一致需要通过IOT_Shadow_Request_Add_Delta_Property接口将当前值添加到请求中，<br>
然后将该请求送到云平台去掉期望值。

回调函数示例 (samples\shadow\shadow_sample.c)

```
//当设备直接按照desired字段中的属性值更新时不需要上报
	void RegCallback_update(void *pClient, RequestParams *pParams, char *pJsonValueBuffer, uint32_t valueLength, DeviceProperty *pProperty)
	{    
		LOG_DEBUG("key:%s val:%s\n",pProperty->key, pJsonValueBuffer);    
		IOT_Shadow_Direct_Update_Value(pJsonValueBuffer, pProperty);    
		return;
	}

//当设备没有完全按照desired字段中的属性更新时,需要将当前真实值上报
	void RegCallback_hold(void *pClient, RequestParams *pParams, char *pJsonValueBuffer, uint32_t valueLength, DeviceProperty *pProperty)
	{    
		LOG_DEBUG("key:%s val:%s\n",pProperty->key, pJsonValueBuffer);    
		int num = 10;    
		pProperty->data = &num;
		IOT_Shadow_Request_Add_Delta_Property(pClient, pParams,pProperty);    
		return;
	}
```

## 影子文档修改请求说明

一个请求只支持做一种操作，支持同时修改多个属性。

## 代码示例 (samples\shadow\shadow_sample.c)

首先配置设备信息，创建设备影子的句柄

```		
	ret = _setup_connect_init_params(&sg_initParams);    
	if(ret != SUCCESS)    
	{        
		HAL_Printf("_setup_connect_init_params fail:%d\n", ret);        
		return ret;    
	}        

	void *mqtt_client = IOT_MQTT_Construct(&sg_initParams);    
	if(mqtt_client == NULL)    
	{        
		HAL_Printf("IOT_MQTT_Construct fail\n");        
		return ERR_PARAM_INVALID;    
	}        

	void *shadow_client = IOT_Shadow_Construct(UIOT_MY_PRODUCT_SN, UIOT_MY_DEVICE_SN, mqtt_client);    
	if(shadow_client == NULL)    
	{        
		HAL_Printf("IOT_Shadow_Construct fail\n");        
		return ERR_PARAM_INVALID;    
	}
```

在操作设备影子文档前需要先注册当前设备有的属性和属性回调函数，属性回调函数需要用户自己实现

```
	DeviceProperty *Property1 = (DeviceProperty *)HAL_Malloc(sizeof(DeviceProperty));    
	int32_t num1 = 18;    
	char str1[6] = "data1";    
	Property1->key= str1;    
	Property1->data = &num1;    
	Property1->type = JINT32;    
	ret = IOT_Shadow_Register_Property(sg_pshadow, Property1, RegCallback_hold);     
	if(SUCCESS != ret)    
	{        
		HAL_Printf("Register Property1 fail:%d\n", ret);        
		return ret;    
	}
```

首先同步一下版本号和属性值，防止设备掉电过程中云平台的一些改动没有及时同步导致后面的操作由于设备影子文档版本号不一致而设置失败

```
	/* 先同步一下版本号和设备掉电期间更新的属性 */    
	ret = IOT_Shadow_Get_Sync(sg_pshadow, _update_ack_cb, time_sec, &ack_update);    
	if(SUCCESS != ret)    
	{        
		HAL_Printf("Get Sync fail:%d\n", ret);        
		return ret;    
	}

	while (ACK_NONE == ack_update)
	{        
		IOT_Shadow_Yield(sg_pshadow, MAX_WAIT_TIME_MS);    
	}
```

同步后可以开始做更新或者删除属性的操作了

```
	/* update */        
	ack_update = ACK_NONE;    
	ret = IOT_Shadow_Update(sg_pshadow, _update_ack_cb, time_sec, &ack_update, 6, Property1, Property2, Property3, Property4, Property5, Property6);    
	if(SUCCESS != ret)    
	{        
		HAL_Printf("Update Property1 Property2 Property3 Property4 Property5 Property6 fail:%d\n", ret);        
		return ret;    
	}     

	while (ACK_NONE == ack_update)
	{        
		IOT_Shadow_Yield(sg_pshadow, MAX_WAIT_TIME_MS);    
	}
```
操作完后释放本地资源

```
	HAL_Free(Property1);    
	HAL_Free(Property2);    
	HAL_Free(Property3);    
	HAL_Free(Property4);    
	HAL_Free(Property5);    
	HAL_Free(Property6);    
	IOT_Shadow_Destroy(sg_pshadow);
```
# Shadow接口详细说明文档

## IOT_Shadow_Construct

初始化，创建Shadow连接句柄

```
void *IOT_Shadow_Construct(const char *product_sn, const char *device_sn, void *ch_signal);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| product_sn | const char * | 输入 | 指向产品序列号的指针 |
| device_sn | const char * | 输入 | 指向设备序列号的指针 |
| ch_signal | void * | 输入 | MQTT的句柄 |
| ret | void * | 返回 | 设备影子的句柄 |

## IOT_Shadow_Destroy

销毁影子文档连接句柄。

```
void IOT_Shadow_Destroy(void *handle);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄的指针 |

## IOT_Shadow_Yield

在当前线程为底层为Shadow客户端让出一定CPU执行时间

```
int IOT_Shadow_Yield(void *handle, uint32_t timeout_ms)
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| timeout_ms | uint32_t | 输入 | 等待时间，单位是ms |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_Register_Property

添加本地设备的属性

```
int IOT_Shadow_Register_Property(void *handle, DeviceProperty *pProperty, OnPropRegCallback callback);
```
### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| pProperty | DeviceProperty * | 输入 | 设备属性 |
| callback | OnPropRegCallback | 输入 | 属性的处理回调函数，用于决定和服务器上期望的属性值不一致时取哪个 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_UnRegister_Property

注销本地设备的属性

```
int IOT_Shadow_UnRegister_Property(void *handle, DeviceProperty *pProperty);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| pProperty | DeviceProperty * | 输入 | 设备属性 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_Get_Sync

获取云服务器上的设备影子文档，并同步更新属性和影子文档版本号

```
int IOT_Shadow_Get_Sync(void *handle, OnRequestCallback request_callback, uint32_t timeout_sec, void *user_context);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| request_callback | OnRequestCallback | 输入 | 请求的回调函数 |
| timeout_sec | uint32_t | 输入 | 超时时间，单位为秒 |
| user_context | RequestParams * | 输入 | 请求回调函数入参 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_Update

更新云服务器上的设备影子文档属性，可以一次更新多个属性，变长入参中的属性个数要和property_count一致。

```
int IOT_Shadow_Update(void *handle, OnRequestCallback request_callback, uint32_t timeout_sec, void *user_context, int property_count, ...) ;
```

### 参数列表
| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| request_callback | OnRequestCallback | 输入 | 请求的回调函数 |
| timeout_sec | uint32_t | 输入 | 超时时间，单位为秒 |
| user_context | RequestParams * | 输入 | 请求回调函数入参 |
| property_count | int | 输入 | 变长入参的个数 |
| ... | DeviceProperty * | 输入 | 设备属性 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_Update_And_Reset_Version

更新云服务器上的设备影子文档属性并清零版本号，可以一次更新多个属性，变长入参中的属性个数要和property_count一致。

```
int IOT_Shadow_Update_And_Reset_Version(void *handle, OnRequestCallback request_callback, uint32_t timeout_sec, void *user_context, int property_count, ...) ;
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| request_callback | OnRequestCallback | 输入 | 请求回调函数 |
| timeout_Sec | uint32_t | 输入 | 请求超时时间，单位为秒 |
| user_context | void * | 输入 | 请求结果 |
| property_count | int | 输入 | 变长入参的个数 |
| ... | DeviceProperty * | 输入 | 设备属性 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_Delete

删除云服务器上的设备影子文档属性，可以一次删除多个属性，变长入参中的属性个数要和property_count一致

```
int IOT_Shadow_Delete(void *handle, OnRequestCallback request_callback, uint32_t timeout_sec, void *user_context, int property_count, ...) ;
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| request_callback | OnRequestCallback | 输入 | 请求回调函数 |
| timeout_Sec | uint32_t | 输入 | 请求超时时间，单位为秒 |
| user_context | void * | 输入 | 请求结果 |
| property_count | int | 输入 | 变长入参的个数 |
| ... | DeviceProperty * | 输入 | 设备属性 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |


## IOT_Shadow_Delete_All

删除云服务器上的设备影子文档中的全部属性

```
int IOT_Shadow_Delete_All(void *handle, OnRequestCallback request_callback, uint32_t timeout_sec, void *user_context) ;
```

### 参数列表 | 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| request_callback | OnRequestCallback | 输入 | 请求的回调函数 |
| timeout_sec | uint32_t | 输入 | 超时时间 |
| user_context | RequestParams * | 输入 | 请求回调函数入参 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_Request_Add_Delta_Property

往请求中增加需要修改的属性

```
int IOT_Shadow_Request_Add_Delta_Property(void *handle, RequestParams *pParams, DeviceProperty *pProperty);
```
### 参数列表
| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | 影子文档句柄 |
| pParams | RequestParams * | 输入 | 设备影子修改请求 |
| pProperty | DeviceProperty * | 输入 | 设备属性 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |

## IOT_Shadow_Direct_Update_Value

使用包含属性键值的字符串中的值更新对应属性值

```
int IOT_Shadow_Direct_Update_Value(char *value, DeviceProperty *pProperty);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| value | char * | 输入 | 设备影子文档desired中解析出来的包含属性键值的字符串 |
| pProperty | DeviceProperty * | 输入 | 设备属性 |
| ret | int | 返回 | 成功返回SUCCESS,<br>FAILURE表示失败 |
