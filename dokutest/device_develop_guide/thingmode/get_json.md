{{indexmenu_n>2}}

====== 获取物模型JSON文档 ======

获取物模型定义JSON文档是指获取在[[|控制台操作指南-物模型]]定义的所有属性、命令、事件的JSON描述文档。

===== 具体流程 =====

<HTML><ol></HTML>
<HTML><li></HTML><HTML><p></HTML>请求获取物模型JSON文档；\\
设备向Topic ''%%/$system/${ProductSN}/${DeviceSN}/tmodel/template/get%%''发布一条消息，消息格式为：<HTML></p></HTML>
<code>
{
  "RequestID": "100"
} 

</code>
<HTML><p></HTML>参数解释：<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>RequestID：请求消息的ID号，为字符串型，根据RequestID确定一条请求以及响应的一一对应性。<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>下发JSON文档； 云平台向Topic ''%%/$system/${ProductSN}/${DeviceSN}/tmodel/template/get_reply%%''下发一条消息，消息格式为：<HTML></p></HTML>
<code>
{
  "RetCode": 0,
  "RequestID": "100",
  "Template": {...}
}

</code>
<HTML><p></HTML>参数解释：<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>RetCode：返回码，具体参考[[|通用返回码]]；<HTML></li></HTML>
<HTML><li></HTML>RequestID：返回消息的ID，对应请求消息ID；<HTML></li></HTML>
<HTML><li></HTML>Template：物模型的JSON描述文档，这里省略，参考[[|物模型示例]];<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML><HTML></ol></HTML>

