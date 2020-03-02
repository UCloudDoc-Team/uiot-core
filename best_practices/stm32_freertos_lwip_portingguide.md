# 基于STM32+FreeRTOS+LWIP的SDK移植

## STM32F767

* Arm M7核 216 Mhz

* 2 Mbytes Falsh

* 512 Kbytes SRAM 

* IEEE-802.3 网络接口

* 支持ST-LINK调试

我们将在STM32F767上移植Freertos实时操作系统，并在Freertos系统上运行我们的SDK，本次仅演示移植MQTT收发消息部分。

## 使用STM32CubeMX工具生成新工程

新建工程

![](/images/STM32新建工程.png)

选择当前使用的模块STM32F767ZI开始工程

![](/images/STM32选择芯片.png)

设置时钟

![](/images/SYS设置时钟.png)

选择定时器

![](/images/SYS选择定时器.png)

设置接口

![](/images/Connect设置网络.png)

![](/images/connect设置调试串口.png)

![](/images/connect设置USB.png)

选择使用freertos操作系统

![](/images/操作系统freertos.png)

需要使用动态申请内存，把堆栈改大一点

![](/images/操作系统动态申请内存.png)

网络连接部分需要使用LWIP库

![](/images/使能LWIP.png)

选择必要的网络协议

![](/images/协议选择.png)

参考钟设置

![](/images/时钟选择.png)

填写项目名称等信息，点击生成代码

![](/images/填写项目信息.png)

生成的代码可以直接使用IAR打开

![](/images/打开工程.png)

到这里STM32的代码就准备完成了，下面开始抽取SDK的代码，只需要抽取MQTT部分以及公共库那部分代码。

![](/images/MQTT抽取代码.png)

其中sdk-impl文件夹部分只需要部分头文件

![](/images/sdk-impl部分.png)

该文件夹中有freertos的底层实现函数

![](/images/MQTT抽取代码操作系统部分.png)

把抽取出的文件加入到前面生成的IAR工程中，编译运行即可，输出如下图

![](/images/打印输出.png)
