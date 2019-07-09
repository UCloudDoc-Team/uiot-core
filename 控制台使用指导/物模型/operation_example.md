{{indexmenu_n>3}}

### 功能定义示例
物模型以JSON格式进行表述，下面为一个物模型JSON模板：
==几个问题：PropertyID、EventID、CommandID怎么获取==

```JSON
{
  "Property": [
    {
      "PropertyID": 2342, 
      "Identifier": "air_condition_temperature",
      "Name": "空调温度",
      "AccessMode": "rw",
      "Description": "temperature",
      "DataType": {
        "Type": "int32",
        "Spec": {
          "Min": 0,
          "Max": 100,
          "Step": 1,
          "UnitName": "摄氏度"
        }
      }
    }
  ], 
  "Event": [
    {
      "EventID": 1234, 
      "Identifier": "alarm",
      "Name": "alarm",
      "Description": "空调告警",
      "Type": "warning", 
      "Output": [
        {
          "Identifier": "errorCode",
          "Name": "错误码",
          "DataType": {
            "Type": "text",
            "Spec": {
              "Length": "255"
            }
          }
        }
      ]
    }
  ], 
  "Command": [
    {
      "CommandID": 1234, 
      "Identifier": "downTemp",
      "Name": "downTemp",
      "Description": "调低温度",
      "Input": [
        {
          "Identifier": "downValue",
          "Name": "调低幅值",
          "DataType": {
            "Type": "int32",
            "Spec": {
              "Min": 0,
              "Max": 100,
              "Step": 1,
              "UnitName": "摄氏度"
            }
          }
        }
      ], 
      "Output": [
        {
          "Identifier": "curTemp",
          "Name": "当前温度",
          "DataType": {
            "Type": "int32",
            "Spec": {
              "Min": 0,
              "Max": 100,
              "Step": 1,
              "UnitName": "摄氏度"
            }
          }
        }
      ]
    }
  ]
}
```



