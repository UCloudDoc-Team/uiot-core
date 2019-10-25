{{indexmenu_n>6}}

# 设备OTA开发

UIoT-Core 支持设备通过 OTA(Over-the-Air Technology) 进行固件升级。本章描述如何利用设备端 C-SDK 提供的API进行设备端 OTA 功能开发。下面的讲解对应于 C-SDK 示例代码 samples/ota/ota_sample.c 。

## 功能说明

- C-SDK 提供支持固件下载及校验的 API，但固件存储以及烧录需要用户在应用程序中实现。

- 建议在 OTA 功能设计之初预留充足的存储容量以便存放固件，同时充分考虑到烧录的风险，如有必要提前设计烧录失败的回退逻辑。

## 开发步骤

### 准备

1. 在控制台创建一个产品和一个设备，替换 ota_sample.c 中的设备四元组信息。

2. 上传一个固件（版本号任选，与示例代码中的 "1.0.0" 不同即可）。

3. 在示例代码启动并上报版本之后，在控制台发起设备升级操作，将设备升级到上传的固件版本。

### 初始化

在使用 OTA 功能之前，首先需要进行初始化，包括 MQTT 客户端的创建、OTA 的初始化以及版本上报。可参照 ota_sample.c 中 main 函数的初始化部分代码。

```
//1. 首先创建MQTT客户端，并与云端建立MQTT连接
void *client = IOT_MQTT_Construct(&init_params);
if (client != NULL) {
    LOG_INFO("MQTT Construct Success");
} else {
    LOG_ERROR("MQTT Construct Failed");
    return FAILURE;
}

//2. OTA 初始化，获取句柄
void *h_ota = IOT_OTA_Init(UIOT_MY_PRODUCT_SN, UIOT_MY_DEVICE_SN, client);
if (NULL == h_ota) {
    LOG_ERROR("init OTA failed");
    return FAILURE;
}

//3. 上报初始版本，未上报版本的设备无法升级
if (IOT_OTA_ReportVersion(h_ota, "1.0.0") < 0) {
    LOG_ERROR("report OTA version failed");
    return FAILURE;
}

//4. （可选）主动请求设备 OTA 信息，用于防止设备离线期间错过 OTA 升级消息等特殊情况
if (IOT_OTA_RequestFirmware(h_ota, "1.0.0") < 0) {
    LOG_ERROR("Request firmware failed");
    return FAILURE;
}
```

### 下载及升级流程

流程包括固件的下载、校验、存储和烧录等步骤。由于硬件平台等差异，用户可根据实际情况仿照示例代码实现整个流程。

```
//打开一个文件，用于存储固件
if (NULL == (fp = fopen("ota.bin", "wb+"))) {
    LOG_ERROR("open file failed");
    return FAILURE;
}

do {
    uint32_t firmware_valid;
    LOG_INFO("wait for ota upgrade command...");
    //接收下行 OTA 消息，如果收到升级信息 IOT_OTA_IsFetching(h_ota) 将会更新为 1
    IOT_MQTT_Yield(client, 100);
    //进入固件下载状态
    if (IOT_OTA_IsFetching(h_ota)) {
        char version[33], md5sum[33];
        uint32_t size_downloaded, size_file;
        do {
            //下载固件至缓冲区
            int len = IOT_OTA_FetchYield(h_ota, buf_ota, OTA_BUF_LEN, 1);
            if (len > 0) {
                //将缓冲区的数据写入文件
                if (1 != fwrite(buf_ota, len, 1, fp)) {
                    LOG_ERROR("write data to file failed");
                    upgrade_fetch_success = false;
                    break;
                }
            } else if (len < 0) {
                LOG_ERROR("download fail rc=%d", len);
                upgrade_fetch_success = false;
                break;
            }

            //获取 OTA 信息
            IOT_OTA_Ioctl(h_ota, OTA_IOCTL_FETCHED_SIZE, &size_downloaded, 4);
            IOT_OTA_Ioctl(h_ota, OTA_IOCTL_FILE_SIZE, &size_file, 4);
            IOT_OTA_Ioctl(h_ota, OTA_IOCTL_MD5SUM, md5sum, 33);
            IOT_OTA_Ioctl(h_ota, OTA_IOCTL_VERSION, version, 33);
            IOT_OTA_Ioctl(h_ota, OTA_IOCTL_VERSION, msg_version, 33);

            IOT_MQTT_Yield(client, 100);
        } while (!IOT_OTA_IsFetchFinish(h_ota));

        //下载固件完成
        if (upgrade_fetch_success) {
            //固件校验
            IOT_OTA_Ioctl(h_ota, OTA_IOCTL_CHECK_FIRMWARE, &firmware_valid, 4);
            if (0 == firmware_valid) {
                LOG_ERROR("The firmware is invalid");
                upgrade_fetch_success = false;
            } else {
                LOG_INFO("The firmware is valid");
                upgrade_fetch_success = true;
            }
        }
        ota_over = 1;
    }

    HAL_SleepMs(2000);
} while(!ota_over);

if (upgrade_fetch_success)
{
    //可在此处处理固件烧录相关操作
    HAL_SleepMs(1000);
    //上报升级成功
    IOT_OTA_ReportSuccess(h_ota, msg_version);
}
```

### 资源释放

固件升级完成后，需要释放 OTA 过程中使用的资源。

```
//关闭文件
fclose(fp);
//释放OTA资源
IOT_OTA_Destroy(h_ota);
//（可选）释放 MQTT Client 资源
IOT_MQTT_Destroy(&client);
```

## API 列表

### IOT_OTA_Init

初始化 OTA 模块

```
void *IOT_OTA_Init(const char *product_sn, const char *device_sn, void *ch_signal);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| product_sn | const char * | 输入 | 指向产品序列号的指针 |
| device_sn | const char * | 输入 | 指向设备序列号的指针 |
| ch_signal | void * | 输入 | 指定的信号通道，目前为 IOT_MQTT_Construct 返回的句柄 |
| ret | void * | 返回值 | 初始化成功，返回句柄；初始化失败，返回 NULL |

### IOT_OTA_Destroy

释放 OTA 相关的资源

```
int IOT_OTA_Destroy(void *handle);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| ret | int | 返回值 | <0: 失败  =0: 成功 |

### IOT_OTA_ReportVersion

向 OTA 服务器报告固件版本信息

```
int IOT_OTA_ReportVersion(void *handle, const char *version);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| version | const char * | 输入 | 以字符串格式指定固件版本 |
| ret | int | 返回值 | <0: 上报失败  >0: 成功，返回对应 publish 的 packet id |

### IOT_OTA_ReportProgress

向 OTA 服务器报告详细进度

```
int IOT_OTA_ReportProgress(void *handle, int progress, IOT_OTA_ProgressState state);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| progress | int | 输入 | 下载或升级进度，范围为 0-100 |
| state | IOT_OTA_ProgressState | 输入 | 当前的 OTA 状态 |
| ret | int | 返回值 | <0: 上报失败  >0: 成功，返回对应 publish 的 packet id |

### IOT_OTA_ReportSuccess

向 OTA 服务器上报升级成功

```
int IOT_OTA_ReportSuccess(void *handle, const char *version);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| version | const char * | 输入 | 以字符串格式指定的当前固件版本，如果版本错误，云端认为固件升级失败 |
| ret | int | 返回值 | <0: 上报失败  >0: 成功，返回对应 publish 的 packet id |

### IOT_OTA_ReportFail

向 OTA 服务器上报失败信息

```
int IOT_OTA_ReportFail(void *handle, IOT_OTA_ReportErrCode err_code);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| err_code | IOT_OTA_ReportErrCode | 输入 | 错误码 |
| ret | int | 返回值 | <0: 上报失败  >0: 成功，返回对应 publish 的 packet id |

### IOT_OTA_IsFetching

检查是否处于下载固件的状态

```
int IOT_OTA_IsFetching(void *handle);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| ret | int | 返回值 | 0: No  1: Yes |

### IOT_OTA_IsFetchFinish

检查固件是否已经下载完成

```
int IOT_OTA_IsFetchFinish(void *handle);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| ret | int | 返回值 | 0: No  1: Yes |

### IOT_OTA_FetchYield

从远程服务器获取固件

```
int IOT_OTA_FetchYield(void *handle, char *buf, size_t buf_len, uint32_t timeout_s);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| buf | char * | 输出 | 指定存储固件数据的缓冲区 |
| buf_len | size_t | 输入 | buf 的长度 |
| timeout_s | uint32_t | 输入 | 超时时间 |
| ret | int | 返回值 | <0: 对应的错误码  0: 在 timeout_s 超时期间内没有任何数据被下载 (0, len] : 在 timeout_s 超时时间内下载数据的长度 |

### IOT_OTA_Ioctl

获取指定的 OTA 信息

```
int IOT_OTA_Ioctl(void *handle, IOT_OTA_CmdType type, void *buf, size_t buf_len);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| type | IOT_OTA_CmdType | 输入 | 指定想要的信息 |
| buf | void * | 输出 | 为数据交换指定缓冲区 |
| buf_len | size_t | 输入 | buf 的长度 |
| ret | int | 返回值 | <0: 失败  0: 成功 |

#### 说明

* 如果 type==OTA_IOCTL_FETCHED_SIZE, 'buf' 需要传入 uint32_t 类型指针, 'buf_len' 需指定为 4

* 如果 type==OTA_IOCTL_FILE_SIZE, 'buf' 需要传入 uint32_t 类型指针, 'buf_len' 需指定为 4

* 如果 type==OTA_IOCTL_MD5SUM, 'buf' 需要传入 buffer, 'buf_len' 需指定为 33

* 如果 type==OTA_IOCTL_VERSION, 'buf' 需要传入 buffer, 'buf_len' 需指定为 OTA_VERSION_LEN_MAX

* 如果 type==OTA_IOCTL_CHECK_FIRMWARE, 'buf' 需要传入 uint32_t 类型指针, 'buf_len'需指定为 4 。返回：0, 固件MD5校验不通过, 固件无效; 1, 固件有效

### IOT_OTA_GetLastError

获取最后一个错误码

```
int IOT_OTA_GetLastError(void *handle);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| ret | int | 返回值 | 对应错误的错误码 |

### IOT_OTA_RequestFirmware

请求固件更新消息。设备离线时，不能接收服务端推送的升级消息，需要通过 MQTT 协议接入物联网平台的设备再次上线后，主动请求固件更新消息

```
int IOT_OTA_RequestFirmware(void *handle, const char *version);
```

#### 参数列表

| 参数 | 数据类型 | 参数类型 | 说明 |
| --- | --- | --- | --- |
| handle | void * | 输入 | IOT_OTA_Init 返回的句柄 |
| version | const char * | 输入 | 以字符串格式指定的当前版本号 |
| ret | int | 返回值 | <0: 上报失败  >0: 成功，返回对应publish的packet id |
