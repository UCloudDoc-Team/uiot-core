# 功能介绍

UCloud IoT通信云平台为海量设备上报数据、控制设备提供安全可靠连接保证，IoT通信云平台基于设备接入、设备管理、规则引擎、设备影子、物模型、文件上传、OTA、设备端SDK、云端API等功能提供一个完整的从设备到平台到应用的解决方案。


## 设备接入

提供广泛的设备接入能力，用户可以方便地通过[设备端SDK](/iot/uiot-core/device_develop_guide/c_sdk_example/csdkquickstart)接入到IoT通信云平台，并且可以按照SDK中的示例代码，快速嵌入自己的业务逻辑实现连接云端的能力。 

提供完善的设备接入方案：

- 提供安全的基于MQTT和MQTT Over TLS的[设备注册](/iot/uiot-core/device_develop_guide/authenticate_devices/what_is_authenticate_devices)、[设备连接](/iot/uiot-core/device_develop_guide/deviceconnect/mqttconnect)机制
- 提供基于HTTP和HTTP Over TLS的[设备注册](/iot/uiot-core/device_develop_guide/authenticate_devices/what_is_authenticate_devices)、[设备连接](/iot/uiot-core/device_develop_guide/deviceconnect/mqttconnect)机制
- 提供基于WebSocket和WebSocket Over TLS的[设备注册](/iot/uiot-core/device_develop_guide/authenticate_devices/what_is_authenticate_devices)、[设备连接](/iot/uiot-core/device_develop_guide/deviceconnect/mqttconnect)机制
- 支持原生的Linux、RTOS(FreeRTOS)的移植
- 支持文件上传功能
- 支持OTA升级功能
- 支持设备影子功能
- 支持物模型功能



## 设备管理

设备管理可以帮助用户了解自己的产品以及设备状态，实时了解设备的激活状态、在线状态。

设备管理提供丰富的管理功能：

- 产品及设备的添加删除、检索功能
- 主题的管理，用户可以自定义主题，并可以轻松变更主题的读写权限
- OTA版本及升级管理，了解设备的版本分布状况，按需升级设备



## 规则引擎

规则引擎可以方便灵活地让设备的消息流转到UCloud平台的其他产品，方便业务数据的打通。  
规则引擎通过类SQL的语法帮助用户针对来自不同产品的Topic数据做筛选与处理。

目前规则引擎支持以下流转方式：

- 流转到云数据库UDB（MongoDB、MySQL），帮助用户实现关系或非关系型数据的持久化
- 流转到Kafka消息队列UKafka，应对海量数据上传，实现消息生产者与消费者的解耦
- 流转到时序数据库UTSDB中，存储海量时序数据，方便以后进行数据分析
- M2M流转到其它Topic，实现设备之间的互通
- 流转到用户自己的UHost ，HTTP内网传输方式，无需外网绕行，安全高效
- 流转到UAI-Inference，利用云端AI进行推理计算



## OTA

OTA可以帮助用户管理设备的版本信息，提供可视化的版本分布分析。

用户可以管理不同产品的多个版本，手动或者批量升级指定的设备到指定的版本。



## 文件上传

提供文件上传管理的功能。文件上传可以帮助视频复核的视频文件、历史记录或打包数据、离线数据实现数据批量上传，方便云端应用直接消费。




## 设备影子

设备影子是保存在平台上的对设备状态进行描述的文档。设备影子包含了设备的属性等信息，可以保存设备的当前状态。设备影子是JSON格式的文档，非常适合属性动态添加和删除的场景。

通过设备影子可以完成上层应用和设备之间的上下行数据交互。

设备影子可以让应用在不关心设备在线状态的情况下，下发控制信息到设备影子。即使设备不在线，设备上线后仍然可以获取到下发的控制信息。这将简化应用服务的逻辑，应用无须先确认设备状态再进行指令下发。

设备也可以将自己的状态发送到设备影子，这样应用无需每次都询问设备来获取设备状态，而是通过设备影子直接获取。



## 物模型

物模型是对设备的规范化抽象，包括设备的属性、命令、事件，物模型提供独立的系统主题（Topic），根据这些Topic进行功能的交互行为。

通过物模型，设备和应用程序之间的上行和下行会有统一的数据格式。其中命令支持同步和异步两种方式，方便应用按需下发指令和获取结果。

