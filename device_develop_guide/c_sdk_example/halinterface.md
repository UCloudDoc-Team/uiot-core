{{indexmenu_n>2}}

# HAL接口详细说明

以下接口需要根据硬件平台由用户自己实现，是上层业务的运行基础。

## HAL_MutexCreate

创建互斥量。用于支持线程同步和互斥。

```
void *HAL_MutexCreate(void);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| ret | void * | 返回 | 创建成功返回Mutex指针，<br>创建失败返回NULL |

## HAL_MutexDestroy

销毁互斥量。

```
void HAL_MutexDestroy(_IN_ void *mutex);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| mutex | void * | 输入 | 互斥量指针 |

## HAL_MutexLock

阻塞式加锁。如果互斥量已被另一个线程锁定和拥有，则调用该函数的线程将阻塞，直到该互斥量变为可用为止。

```
void HAL_MutexLock(_IN_ void *mutex);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| mutex | void * | 输入 | 互斥量指针 |

## HAL_MutexTryLock

非阻塞式加锁。成功锁定互斥量之后返回SUCCESS，如果mutex参数所指定的互斥量已经被锁定，调用该函数将立即返回FAILURE，不会阻塞当前线程。

```
IoT_Error_t HAL_MutexTryLock(_IN_ void *mutex);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| mutex | void * | 输入 | 互斥量指针 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示加锁成功，<br>FAILURE表示失败 |

## HAL_MutexUnlock

释放互斥量。

```
void HAL_MutexUnlock(_IN_ void *mutex);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| mutex | void * | 输入 | 互斥量指针 |

## HAL_Malloc

申请内存块。

```
void *HAL_Malloc(_IN_ uint32_t size);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| size | uint32_t | 输入 | 申请的内存块大小 |
| ret | void * | 返回 | 申请成功返回指向内存首地址的指针, <br>申请失败返回NULL |

## HAL_Free

释放内存块。

```C
void HAL_Free(_IN_ void *ptr);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| ptr | void * | 输入 | 指向要释放的内存块的指针 |

## HAL_Printf

打印函数，向标准输出格式化打印一个字符串。

```
void HAL_Printf(_IN_ const char *fmt, ...);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| fmt | const char * | 输入 | 格式化字符串 |
| ... | 可变类型 | 输入 | 可变参数列表 |

## HAL_Snprintf

打印函数, 向内存缓冲区格式化打印一个字符串。

```
int HAL_Snprintf(_OU_ char *str, _IN_ int len, _IN_ const char *fmt, ...);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| str | char *str | 输出 | 指向字符缓冲区的指针 |
| len | int | 输入 | 缓冲区字符长度 |
| fmt | const char * | 输入 | 格式化字符串 |
| ... | 可变类型 | 输入 | 可变参数列表 |
| ret | int | 返回 | 实际写入缓冲区的字符长度 |

## HAL_Vsnprintf

打印函数, 格式化输出字符串到指定buffer中。

```
int HAL_Vsnprintf(_OU_ char *str, _IN_ int len, _IN_ const char *fmt, _IN_ va_list ap);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| str | char *str | 输出 | 用于存放写入字符串的buffer |
| len | int | 输入 | 允许写入的最大字符串长度 |
| fmt | const char * | 输入 | 格式化字符串 |
| ap | va_list | 输入 | 可变参数列表 |
| ret | int | 返回 | 成功写入的字符串长度 |

## HAL_UptimeMs

检索自系统启动以来已运行的毫秒数。

```
uint64_t HAL_UptimeMs(void);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| ret | uint64_t | 返回 | 设备从上电到当前时刻所经过的毫秒数 |

## HAL_SleepMs

休眠函数。

```
void HAL_SleepMs(_IN_ uint32_t ms);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| ms | uint32_t | 输入 | 休眠时长，单位ms |

## HAL_GetProductSN

获取产品序列号。用于从设备持久化存储（例如FLASH）中读取产品序列号。

```
IoT_Error_t HAL_GetProductSN(_OU_ char productSN[IOT_PRODUCT_SN_LEN + 1]);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| productSN | char[] | 输出 | 存放产品序列号的字符串缓冲区 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示获取成功，<br>FAILURE表示获取失败 |

## HAL_GetProductSecret

获取产品密钥。用于从设备持久化存储（例如FLASH）中读取产品密钥。

```
IoT_Error_t HAL_GetProductSecret(_OU_ char productSecret[IOT_PRODUCT_SECRET_LEN + 1]);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| productSecret | char[] | 输出 | 存放产品密钥的字符串缓冲区 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示获取成功，<br>FAILURE表示获取失败 |

## HAL_GetDeviceSN

获取设备序列号。用于从设备持久化存储（例如FLASH）中读取设备序列号。

```
IoT_Error_t HAL_GetDeviceSN(_OU_ char deviceSN[IOT_DEVICE_SN_LEN + 1]);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| deviceSN | char[] | 输出 | 存放设备序列号的字符串缓冲区 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示获取成功，<br>FAILURE表示获取失败 |

## HAL_GetDeviceSecret

获取设备密钥。用于从设备持久化存储（例如FLASH）中读取设备密钥。

```
IoT_Error_t HAL_GetDeviceSecret(_OU_ char deviceSecret[IOT_DEVICE_SECRET_LEN + 1]);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| deviceSecret | char[] | 输出 | 存放设备密钥的字符串缓冲区 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示获取成功，<br>FAILURE表示获取失败 |

## HAL_SetProductSN

设置产品序列号。用于将产品序列号烧写到设备持久化存储（例如FLASH）中，以备后续使用。

```
IoT_Error_t HAL_SetProductSN(_IN_ const char *pProductSN);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pProductSN | const char * | 输入 | 指向产品序列号字符串的指针 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示设置成功，<br>FAILURE表示设置失败 |

## HAL_SetProductSecret

设置产品密钥。用于将产品密钥烧写到设备持久化存储（例如FLASH）中，以备后续使用。

```
IoT_Error_t HAL_SetProductSecret(_IN_ const char *pProductSecret);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pProductSecret | const char * | 输入 | 指向产品密钥字符串的指针 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示设置成功，<br>FAILURE表示设置失败 |

## HAL_SetDeviceSN

设置设备序列号。用于将设备序列号烧写到设备持久化存储（例如FLASH）中，以备后续使用。

```
IoT_Error_t HAL_SetDeviceSN(_IN_ const char *pDeviceSN);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pDeviceSN | const char * | 输入 | 指向设备序列号字符串的指针 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示设置成功，<br>FAILURE表示设置失败 |

## HAL_SetDeviceSecret

设置设备密钥。用于将设备密钥烧写到设备持久化存储（例如FLASH）中，以备后续使用。

```
IoT_Error_t HAL_SetDeviceSecret(_IN_ const char *pDeviceSecret);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| pDeviceSecret | const char * | 输入 | 指向设备密钥字符串的指针 |
| ret | IoT_Error_t | 返回 | 返回SUCCESS表示设置成功，<br>FAILURE表示设置失败 |

## HAL_Timer_Expired

判断定时器时间是否已经过期。

```
bool HAL_Timer_Expired(_IN_ Timer *timer);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| timer | Timer * | 输入 | 定时器结构体 |
| ret | bool | 返回 | 返回true表示定时器过期，<br>返回false表示定时器未过期 |

## HAL_Timer_Countdown_ms

根据timeout时间开启定时器计时, 单位: ms

```
void HAL_Timer_Countdown_ms(_IN_ Timer *timer, _IN_ uint32_t timeout_ms);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| timer | Timer * | 输入 | 定时器结构体 |
| timeout_ms | uint32_t | 输入 | 超时时间, 单位: ms |

## HAL_Timer_Countdown

根据timeout时间开启定时器计时, 单位: s

```
void HAL_Timer_Countdown(_IN_ Timer *timer, _IN_ uint32_t timeout);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| timer | Timer * | 输入 | 定时器结构体 |
| timeout | uint32_t | 输入 | 超时时间, 单位: s |

## HAL_Timer_Remain_ms

检查给定定时器剩余时间, 单位: ms

```
uint32_t HAL_Timer_Remain_ms(_IN_ Timer *timer);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| timer | Timer * | 输入 | 定时器结构体 |
| ret | uint32_t | 返回 | 定时器剩余时间, 单位: ms |

## HAL_Timer_Init

初始化定时器结构体。

```
void HAL_Timer_Init(_IN_ Timer *timer);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| timer | Timer * | 输入 | 定时器结构体 |

## HAL_TLS_Connect

建立TLS连接。根据指定的HOST地址, 服务器端口号和证书文件建立TLS连接, 返回对应的连接句柄。

```
uintptr_t HAL_TLS_Connect(_IN_ const char *host, _IN_ uint16_t port, _IN_ const char *ca_crt, _IN_ size_t ca_crt_len);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| host | const char * | 输入 | 指定的TLS服务器网络地址 |
| port | uint16_t | 输入 | 指定的TLS服务器端口 |
| ca_crt | const char * | 输入 | 指向X.509证书的指针 |
| ca_crt_len | size_t | 输入 | 证书字节长度 |
| ret | uintptr_t | 返回 | 创建成功返回TLS连接句柄，<br>创建失败返回NULL |

## HAL_TLS_Disconnect

断开TLS连接, 并释放相关对象资源。

```
int32_t HAL_TLS_Disconnect(_IN_ uintptr_t handle);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | uintptr_t | 输入 | TLS连接句柄 |
| ret | int32_t | 返回 | 成功返回SUCCESS，<br>失败返回FAILURE |

## HAL_TLS_Write

向指定的TLS连接写入数据。此接口为同步接口, 如果在超时时间内写入了参数len指定长度的数据则立即返回, 否则在超时时间到时返回。

```
int32_t HAL_TLS_Write(_IN_ uintptr_t handle, _IN_ unsigned char *buf, _IN_ size_t len, _IN_ uint32_t timeout_ms);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | uintptr_t | 输入 | TLS连接句柄 |
| buf | unsigned char * | 输入 | 指向数据发送缓冲区的指针 |
| len | size_t | 输入 | 数据发送缓冲区的字节大小 |
| timeout_ms | uint32_t | 输入 | 超时时间，单位: ms |
| ret | int32_t | 返回 | <0: TLS写入错误<br> =0: TLS写超时, 且没有写入任何数据<br> >0: TLS成功写入的字节数 |

## HAL_TLS_Read

从指定的TLS连接读取数据, 此接口为同步接口, 如果在超时时间内读取到参数len指定长度的数据则立即返回, 否则在超时时间到时返回。

```
int32_t HAL_TLS_Read(_IN_ uintptr_t handle, _OU_ unsigned char *buf, _IN_ size_t len, _IN_ uint32_t timeout_ms);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | uintptr_t | 输入 | TLS连接句柄 |
| buf | unsigned char * | 输出 | 指向数据接收缓冲区的指针 |
| len | size_t | 输入 | 数据接收缓冲区的字节大小 |
| timeout_ms | uint32_t | 输入 | 超时时间，单位: ms |
| ret | int32_t | 返回 | <0: TLS读取错误<br> =0: TLS读超时, 且没有读取任何数据<br> >0: TLS成功读取的字节数 |

## HAL_TCP_Connect

建立TCP连接。根据指定的HOST地址, 服务器端口号建立TCP连接, 返回对应的连接句柄，需要注意的是如果创建失败，返回的是创建失败返回(uintptr_t)(-1)。

```
uintptr_t HAL_TCP_Connect(_IN_ const char *host, _IN_ uint16_t port);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| host | const char * | 输入 | 指定的TCP服务器网络地址 |
| port | uint16_t | 输入 | 指定的TCP服务器端口 |
| ret | uintptr_t | 返回 | 创建成功返回TCP连接句柄，<br>创建失败返回(uintptr_t)(-1) |

## HAL_TCP_Disconnect

断开TCP连接, 并释放相关对象资源。

```
int32_t HAL_TCP_Disconnect(_IN_ uintptr_t fd);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| fd | uintptr_t | 输入 | TCP连接句柄 |
| ret | int32_t | 返回 | 成功返回SUCCESS，<br>失败返回FAILURE |

## HAL_TCP_Write

向指定的TCP连接写入数据。此接口为同步接口, 如果在超时时间内写入了参数len指定长度的数据则立即返回, 否则在超时时间到时返回。

```
int32_t HAL_TCP_Write(_IN_ uintptr_t fd, _IN_ unsigned char *buf, _IN_ size_t len, _IN_ uint32_t timeout_ms);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| fd | uintptr_t | 输入 | TCP连接句柄 |
| buf | unsigned char * | 输入 | 指向数据发送缓冲区的指针 |
| len | size_t | 输入 | 数据发送缓冲区的字节大小 |
| timeout_ms | uint32_t | 输入 | 超时时间，单位: ms |
| ret | int32_t | 返回 | <0: TCP写入错误<br> =0: TCP写超时, 且没有写入任何数据<br> >0: TCP成功写入的字节数 |

## HAL_TCP_Read

从指定的TCP连接读取数据。此接口为同步接口, 如果在超时时间内读取到参数len指定长度的数据则立即返回, 否则在超时时间到时返回。

```
int32_t HAL_TCP_Read(_IN_ uintptr_t fd, _OU_ unsigned char *buf, _IN_ size_t len, _IN_ uint32_t timeout_ms);
```

### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| fd | uintptr_t | 输入 | TCP连接句柄 |
| buf | unsigned char * | 输出 | 指向数据接收缓冲区的指针 |
| len | size_t | 输入 | 数据接收缓冲区的字节大小 |
| timeout_ms | uint32_t | 输入 | 超时时间，单位: ms |
| ret | int32_t | 返回 | <0: TCP读取错误<br> =0: TCP读超时, 且没有读取任何数据<br> >0: TCP成功读取的字节数 |

