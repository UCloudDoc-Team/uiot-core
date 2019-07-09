{{indexmenu_n>2}}

### 设备影子相关操作
对设备影子的操作包括：
- 设备上报状态更新设备影子；
- 应用程序更新设备影子期望值，对设备进行属性设置；
- 应用程序获取设备影子状态；
- 应用程序关闭/开启设备影子；

<br>

设备影子版本号的相关说明：   
- 设备影子每次更新，无论是云端应用还是设备端，都会发生版本的增加，每次+1；
- 设备影子的版本号由平台唯一维护；
- 设备更新属性的版本号必须和平台的设备影子的版本号一致才能上报，否则平台会下发`control`方法，并跟随平台设备影子的版本号；
- 设备影子的版本号为32位整型（int32），设备端需要维护好，特别是发生溢出翻转时；


#### 设备影子涉及的topic
Topic | 权限|描述
|---|---|---
|/$system/${ProductSN}/${DeviceSN}/shadow/upstream |发布|更新设备影子
|/$system/${ProductSN}/${DeviceSN}/shadow/downstream | 订阅| 设置期望值
|/$system/${ProductSN}/${DeviceSN}/shadow/get|发布|获取设备影子



#### 应用用例
假设设备拥有`temperature`和`humidity`两个属性，云端应用可以发送期望温度值给设备端。

#### 设备更新设备影子状态
1. 第一次需要获取当前设备影子的版本号。随便使用一个版本号上报当前状态，平台端会返回一个全量的设备影子的control包。
```
Pub Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream"

{
	"Method": "update",
	"St": {
		"Reported": {
			"temperature": 26.0,
			"humidity": 57.0,
			"smoke": 5.7
		}
	},
	"Version": 0
}
```
2. 平台返回全量设备影子的`control`方法，里面会跟随版本号，`Retcode`为`100026`表示版本冲突，设备需要根据当前情况对其中内容做调整，也可以只关心其版本号。
```
Sub Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream

{
	"Method": "control",
	"Payload": {
		"Retcode": 100026,
		"State": {
			"Reported": {
				"humidity": 57,
				"smoke": 5.7,
				"temperature": 26
			},
			"Desired": "{}"
		},
		"Metadata": {
			"Reported": {
				"humidity": {
					"Timestamp": 1557128294
				},
				"smoke": {
					"Timestamp": 1557128294
				},
				"temperature": {
					"Timestamp": 1557128294
				}
			},
			"Desired": "{}"
		}
	},
	"Version": 165256,
	"Timestamp": 1557228324
}
```
参数|说明|
|---|---|--
|Method|表示对设备影子的操作类型，包括update更新/control控制/ reply回复
|Retcode|响应妈，具体可以参考下面的响应码|

响应码|说明|
|---|---|---
|0 |请求成功
|230 |不正确的JSON格式
|230 |消息体缺少 method 信息
|230 |消息体缺少 state 字段
|230 |消息体 version 不是数字
|230 |消息体缺少 desired 字段
|230 |消息体 method 是无效的方法
|100025 |影子文档与消息体 version 版本冲突，顺便返回version的值
|130 |设备影子服务端处理异常


3. 设备使用获得的Version值，重新上报属性值：
```
Pub Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream"

{
	"Method": "update",
	"St": {
		"Reported": {
			"temperature": 26.0,
			"humidity": 57.0,
			"smoke": 5.7
		}
	},
	"Version": 165256
}
```
4. 平台会返回更新成功，同时版本号会增1
```
Sub Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream

{
	"Method": "reply",
	"Payload": {
		"Retcode": 0,
		"State": {
			"Reported": null,
			"Desired": null
		},
		"Metadata": {
			"Reported": null,
			"Desired": null
		}
	},
	"Version": 165257,
	"Timestamp": 1557228324
}
```
5. 之后设备维护好该版本号，当发生版本冲突时，需要重新对齐版本号Versioin。


#### 应用程序更新设备影子期望值
1. 云服务应用通过[API]()，下发需要发给设备端的期望值，
2. 平台更新设备影子并添加`Desired`键值，同时更新版本号，并通过`/$shadow/downstream`下发给设备，假如设备在线的话会立即收到，如果设备不在线需要设备上线后主动做一次版本对齐的操作，版本对齐参考[设备上报状态更新设备影子]()第1步。
```
Sub Topic: /$system/${ProductSN}/${DeviceSN}/shadow/downstream

{
	"Method": "control",
	"Payload": {
		"State": {
			"Reported": {
				"humidity": 57,
				"smoke": 5.7,
				"temperature": 26
			},
			"Desired": {
				"temperature": 30
			}
		},
		"Metadata": {
			"Reported": {
				"humidity": {
					"Timestamp": 1557238829
				},
				"smoke": {
					"Timestamp": 1557238829
				},
				"temperature": {
					"Timestamp": 1557238829
				}
			},
			"Desired": {
				"temperature": {
					"timestamp": 1557238800
				}
			}
		}
	},
	"Version": 165382,
	"Timestamp": 1557238800
}
```

2. 在线设备收到带有期望值的`control`消息之后，将自身状态值设为期望值（本例中的温度一般是控制恒温加热器）。
3. 设备端状态修改后，需要将设备影子的`Desired`键置空。
```
Pub Topic：/$system/${ProductSN}/${DeviceSN}/shadow/upstream"

{
	"Method": "update",
	"St": {
		"Desired": "null"
	},
	"Version": 165382
}
```
4. 平台会更新设备影子文档，清除设备影子`State`和`Metadata`中的`Desired`字段，同时版本号增1，此时设备影子文档更新为
```
{
	"State": {
		"Reported": {
			"humidity": 57,
			"smoke": 5.7,
			"temperature": 26
		}
	},
	"Metadata": {
		"Reported": {
			"humidity": {
				"Timestamp": 1557239829
			},
			"smoke": {
				"Timestamp": 1557239829
			},
			"temperature": {
				"Timestamp": 1557239829
			}
		}
	},
	"Timestamp": 1557239800,
	"Version": 165383
}
```
5. 平台会下发置空成功消息给设备
```
？？？？？？
```
6. 如果设备不在线，需要在设备上线后的第一时间拉取设备影子，检查`State`和`Metadata`中的`Desired`字段，然后根据自身情况以及时间戳决定是否需要更新设备属性。
设备上线后的拉取方法可以参考[设备上报状态更新设备影子]()，利用版本冲突，平台会下发全量的设备影子，此时设备拿到了全量的设备影子。


#### 应用程序获取设备影子状态
应用程序直接通过[云端API]()可以获取设备影子状态。



#### 应用程序关闭/开启设备影子
应用程序直接通过[云端API]()可以关闭/开启设备影子状态。