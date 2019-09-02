{{indexmenu_n>7}}

# 常见问题

## 编译问题

##### 编译出现**undefined reference**错误

```
[CC] HAL_OS_linux.o                     <= HAL_OS_linux.c                                    
[CC] HAL_TCP_linux.o                    <= HAL_TCP_linux.c                                    
[CC] HAL_Timer_linux.o                  <= HAL_Timer_linux.c                                    
[CC] HAL_TLS_mbedtls.o                  <= HAL_TLS_mbedtls.c                                    
[AR] libiot_platform.a                  <= HAL_OS_linux.o                                    
                                           HAL_TCP_linux.o
                                           HAL_Timer_linux.o
                                           HAL_TLS_mbedtls.o
/home/os/projects/ucloud/ucloud-iot-device-sdk-c-master/output/release/lib/libiot_platform.a(HAL_OS_linux.o): In function `HAL_UptimeMs':
HAL_OS_linux.c:(.text+0x102): undefined reference to `clock_gettime'
collect2: error: ld returned 1 exit status
make: *** [mqtt_sample] Error 1
```

**错误分析**

该问题是由于SDK的linux HAL层用到了linux librt实时库（real time），编译器找不到系统头文件<time.h>，需要添加该库。

**解决方法**

修改文件：**${SDK_DIR}/tools/scripts/parse_make_settings.mk**


将line32,35

```
CFLAGS  += -DFORCE_SSL_VERIFY -DENABLE_LOG_ERR -DENABLE_LOG_WARN -DENABLE_LOG_INFO
ifeq (debug,$(strip $(BUILD_TYPE)))
CFLAGS  += -DENABLE_LOG_DEBUG -DENABLE_IOT_TRACE
endif
```

修改为：

```
CFLAGS  += -DFORCE_SSL_VERIFY -DENABLE_LOG_ERR -DENABLE_LOG_WARN -DENABLE_LOG_INFO -lrt
ifeq (debug,$(strip $(BUILD_TYPE)))
CFLAGS  += -DENABLE_LOG_DEBUG -DENABLE_IOT_TRACE -lrt
endif
```

#### 编译出现**g++ not found**错误

```
[AR] libiot_platform.a                  <= HAL_OS_linux.o                                    
                                           HAL_TCP_linux.o
                                           HAL_Timer_linux.o
                                           HAL_TLS_mbedtls.o
mv mqtt_sample /home/os/projects/ucloud/ucloud-iot-device-sdk-c-master/output/release/bin
make[1]: g++: Command not found
make[1]: *** [lib] Error 127
make: *** [gtest] Error 2
os@os:~/projects/ucloud/ucloud-iot-device-sdk-c-master$ 
```

**错误分析**

ARM平台使用交叉编译时，需要添加编译器。
由于SDK使用了googletest框架作为用例测试，而googletest使用的是C++编写的，所以需要C++编译器。

**解决方法**
关闭googletest模块；

修改**${SDK_DIR}/make.settings**


将line24

```
FEATURE_SDK_TESTS_ENABLED               = y     # 是否打开SDK测试用例编译
```

修改为：

```
FEATURE_SDK_TESTS_ENABLED               = n     # 是否打开SDK测试用例编译
```


#### 编译出现**C99**错误

```
[CC] mqtt_client_common.o               <= mqtt_client_common.c                                    
/root/ucloud/ucloud-iot-device-sdk-c/src/mqtt/src/mqtt_client_common.c: In function ‘_handle_suback_packet’:
/root/ucloud/ucloud-iot-device-sdk-c/src/mqtt/src/mqtt_client_common.c:925:5: error: ‘for’ loop initial declarations are only allowed in C99 mode
     for (int j = 0; j <  count; j++) {
     ^
/root/ucloud/ucloud-iot-device-sdk-c/src/mqtt/src/mqtt_client_common.c:925:5: note: use option -std=c99 or -std=gnu99 to compile your code
make: *** [/root/ucloud/ucloud-iot-device-sdk-c/src/mqtt/src/mqtt_client_common.o] Error 1
```

**错误分析**

编译器不支持C99风格代码。

**解决方法**

添加C99支持。

修改**${SDK_DIR}/make.settings**

将line32,35

```
CFLAGS  += -std=gnu99 -DFORCE_SSL_VERIFY -DENABLE_LOG_ERR -DENABLE_LOG_WARN -DENABLE_LOG_INFO
ifeq (debug,$(strip $(BUILD_TYPE)))
CFLAGS  += -DENABLE_LOG_DEBUG -DENABLE_IOT_TRACE
endif
```

修改为：

```
CFLAGS  += -std=gnu99 -DFORCE_SSL_VERIFY -DENABLE_LOG_ERR -DENABLE_LOG_WARN -DENABLE_LOG_INFO
ifeq (debug,$(strip $(BUILD_TYPE)))
CFLAGS  += -std=gnu99 -DENABLE_LOG_DEBUG -DENABLE_IOT_TRACE
endif
```

