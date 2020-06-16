# 功能定义导出文件
## 导出功能定义文件

### 操作步骤

1. [注册](https://passport.ucloud.cn/#register)UCloud云服务，如已注册请直接第2步；
2. 登录进入UCloud[物联网平台](https://console.ucloud.cn/uiot)；
3. 选择相应的产品，进入[产品详情](uiot-core/console_guide/product_device/create_products#产品详情)；
4. 选择<功能定义>标签；
5. 关闭<产品发布状态>按钮；
   - 产品发布状态：产品发布状态为打开表示当前产品已发布，不能再对物模型或Topic等做修改；
6. 点击<导出物模型>，获得json格式的物模型文件

![添加物模型](/images/物模型导出.png)

### 物模型文件示例

下面为一个物模型JSON模板：
可以参考设备物模型开发[获取物模型JSON文档](uiot-core/device_develop_guide/thingmode/get_json)获取定义的物模型。

JSON文档中的PropertyID、EventID、CommandID由系统生成，云端应用可以根据此ID值修改物模型的定义。

```
{
  "Template": {
    "Property": [{
      "PropertyID": 94,
      "Identifier": "temperature",
      "Name": "温度",
      "AccessMode": "rw",
      "Description": "温度属性。",
      "DataType": {
        "Type": "int32",
        "Spec": {
          "Max": 100,
          "Min": -40,
          "Step": 1,
          "UnitName": "摄氏度"
        }
      }
    }],
    "Event": [{
      "EventID": 43,
      "Identifier": "alarm",
      "Name": "空调告警",
      "Description": "空调告警",
      "Type": "warning",
      "Output": [{
        "Identifier": "alarmcode",
        "Name": "报警码",
        "DataType": {
          "Type": "int32",
          "Spec": {
            "Max": 600,
            "Min": 0,
            "Step": 1,
            "UnitName": ""
          }
        }
      }]
    }],
    "Command": [{
      "CommandID": 53,
      "Name": "调低温度",
      "Identifier": "downtemperature",
      "Description": "命令",
      "Output": [{
        "Identifier": "nowvalue",
        "Name": "调低后温度",
        "DataType": {
          "Type": "int32",
          "Spec": {
            "Max": 100,
            "Min": -40,
            "Step": 1,
            "UnitName": "摄氏度"
          }
        }
      }],
      "Input": [{
        "Identifier": "downvalue",
        "Name": "调低温度值",
        "DataType": {
          "Type": "int32",
          "Spec": {
            "Max": 100,
            "Min": 0,
            "Step": 1,
            "UnitName": "摄氏度"
          }
        }
      }]
    }]
  }
}
```



## 导入功能定义文件

### 操作步骤

1. [注册](https://passport.ucloud.cn/#register)UCloud云服务，如已注册请直接第2步；

2. 登录进入UCloud[物联网平台](https://console.ucloud.cn/uiot)；

3. 选择相应的产品，进入[产品详情](uiot-core/console_guide/product_device/create_products#产品详情)；

4. 选择<功能定义>标签；

5. 关闭<产品发布状态>按钮；

   - 产品发布状态：产品发布状态为打开表示当前产品已发布，不能再对物模型或Topic等做修改；

6. 点击<导入物模型>，将修改好的json文件上传。上传成功后，功能定义列表展示的属性、命令、事件为文件中定义的功能。

   注：导出的物模型文件会覆盖该产品已经定义的功能

![添加物模型](/images/物模型导入.png)

