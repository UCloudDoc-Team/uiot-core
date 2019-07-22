{{indexmenu_n>1}}

# 什么是物模型（功能定义）
物模型是对产品的抽象，通过物模型可以完整的表述产品所具有的功能，包括属性、命令和事件。属性可读可写，也就是说属性值可以上报，也可以下行修改；命令是由云应用下发控制指令到设备，设备可以有返回值；事件是突发或者非常规情况，只有上报，可以带参数，不能修改。

物模型是通过JSON文件表述的，完整地表述了现实中的一个实际产品，比如智能空调，属性就包括温度、湿度的上报和对温度、湿度的修改；命令比如温度调低5°，设备可以返回调用成功过与否；事件是只读的，比如压缩机故障等异常信息。


通过物模型，设备和应用程序之间的上行和下行交互会有统一的数据规范。其中命令还支持同步和异步两种方式，支持输入输出参数，方便应用服务实时控制设备并返回结果。


功能 | 描述
---|---
属性| 一般是指设备运行时的状态，比如环境的温度和湿度，属性可读可写；
命令 | 命令是指对设备的下行控制并完成某个动作，分为同步和异步。命令不同于属性的设置，命令通常是一次性操作，比如旋转摄像头30°、调低温度等；
事件 | 事件是指需要即时被外部知晓的信息，可以包含多个输出参数。事件不同于属性上报，属性上报通常是普通信息的，而事件通常是突发性的告警或通知信息，比如故障告警、阈值超限等；

