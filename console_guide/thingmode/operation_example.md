# 功能定义示例
物模型以JSON格式进行表述，下面为一个物模型JSON模板：
可以参考设备物模型开发[获取物模型JSON文档](../../device_develop_guide/thingmode/get_json)获取定义的物模型。

JSON文档中的PropertyID、EventID、CommandID由系统生成，云端应用可以根据此ID值修改物模型的定义。

```JSON
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



