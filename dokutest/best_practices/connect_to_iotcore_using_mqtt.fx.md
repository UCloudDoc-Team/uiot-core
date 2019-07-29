{{indexmenu_n>1}}

====== 使用MQTT.fx接入物联网通信云平台 ======

本实践介绍一个完整的利用物联网通信云平台（UIoT-Core）实现应用程序与设备的消息上报和命令下发。

实践基于模拟客户端MQTT.fx，该软件免费使用，可以在其[[http://mqttfx.jensd.de/index.php/download|官方网站下载]]。

本文列举了通过设备影子和自定义Topic实现上行、下行的通信。用户也可以按照该实践完成通过物模型的上行、下行通信。

===== 前提条件 =====

<HTML><ol></HTML>
<HTML><li></HTML><HTML><p></HTML>参考[[|创建产品]]、[[|创建设备]]，获取产品序列号、设备序列号、设备密钥：<HTML></p></HTML>
<code>
ProductSN：qn4hvcjiyqt2069t
DeviceSN：4ythk4cav6ph4310
DeviceSecret：6g7tjlekwf3sqqqj

</code><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>建立连接，本例以[[|静态注册]]的方式建立连接，如需动态注册请参考[[|动态注册]]。<HTML></p></HTML>
<HTML><p></HTML>1） 根据静态连接获取到MQTT登录需要的三要素：''%%ClientID%%''，''%%UserName%%''，''%%Password%%''。<HTML></p></HTML>
^MQTT认证参数^参数值                                                                                                                                                  ^
|ClientID|qn4hvcjiyqt2069t.4ythk4cav6ph4310<html><br></html>''%%规则：${ProductSN}.${DeviceSN}%%''                                                                |
|UserName|qn4hvcjiyqt2069t|4ythk4cav6ph4310|1<html><br></html>''%%规则：${ProductSN}|${DeviceSN}|${authmode}%%''<html><br></html>''%%authmode: 1表示静态注册；2表示动态注册%%''|
|Password|6g7tjlekwf3sqqqj<html><br></html>''%%规则：${DevSecret}%%''                                                                                             |

<HTML><p></HTML>2）参考[[|设备连接]]，获取MQTT Broker连接域名和TLS CA证书：<HTML></p></HTML>
^Broker参数                ^参数值                  ^
|Broker Address          |mqtt-cn-sh2.ucloud.cn|
|Broker Port             |1883                 |
|TLS(CA Certificate file)|[[|root.cer 下载地址]]   |

<HTML><p></HTML>3）打开MQTT.fx软件，连接成功 按照下图的顺序依次输入相应的参数值。<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>输入Broker Address、Broker Port<HTML></li></HTML>
<HTML><li></HTML>输入User Name、 Passwo<HTML></li></HTML>
<HTML><li></HTML>输入TLS证书<HTML></li></HTML>
<HTML><li></HTML>点击<html><Apply></html>，提交配置<HTML></li></HTML>
<HTML><li></HTML>点击<html><Connect></html>，进行连接<HTML></li></HTML><HTML></ul></HTML>

<HTML><p></HTML>{{../images/连接成功.png|连接成功}}<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>输入TLS证书：<HTML></li></HTML><HTML></ul></HTML>

<HTML><p></HTML>{{../images/TLS证书.png|TLS证书}}<HTML></p></HTML><HTML></li></HTML><HTML></ol></HTML>

===== 通过设备影子 =====

设备影子的具体详情参考[[|设备影子]]，本例中设备影子的Topic为：

^Topic                                                       ^权限^描述    ^
|/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/upstream  |发布|更新设备影子|
|/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/downstream|订阅|设置期望值 |

==== 上行测试（发送设备属性） ====

<HTML><ol></HTML>
<HTML><li></HTML><HTML><p></HTML>在MQTT.fx操作界面，点击<html><Publish></html>，输入Topic：''%%/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/upstream%%''；<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>根据[[|设备影子]]文档输入Payload，上报属性''%%"color" : "red"%%''；<HTML></p></HTML>
<code>
{ 
 "Method" : "update" , 
 "State" : { 
     "Reported" : { 
         "color" : "red" 
     } 
 }, 
 "Version" : 0 
}

</code>
<HTML><p></HTML>{{../images/更新设备影子.png|更新设备影子}}<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>在控制台查看设备影子的更新，上行数据上报成功，如图：<HTML></p></HTML>
<HTML><p></HTML>{{../images/设备影子上报成功.png|设备影子上报成功}}<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>也可以在日志里面查看上报成功结果，如图：<HTML></p></HTML>
<HTML><p></HTML>{{../images/设备影子日志上报成功.png|设备影子日志上报成功}}<HTML></p></HTML><HTML></li></HTML><HTML></ol></HTML>

==== 下行测试（设置期望值） ====

<HTML><ol></HTML>
<HTML><li></HTML><HTML><p></HTML>在MQTT.fx操作界面，点击<html><Subscribe></html>，输入Topic：''%%/$system/qn4hvcjiyqt2069t/4ythk4cav6ph4310/shadow/downstream%%''；<HTML></p></HTML>
<HTML><p></HTML>{{../images/订阅消息.png|订阅消息}}<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>下发期望值，有两种方法：\\
① 参考[[|设备影子]]，<编辑>设备影子，输入<html><Desired></html>值：<HTML></p></HTML>
<code>
{
 "color":"green"
}

</code>
<HTML><p></HTML>② 使用云端API进行调用，参考[[|UpdateUIoTCoreDeviceShadow]]，下发需要发给设备端的期望值。\\
UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[[|关于API接入]]，其他参数参考[[|UpdateUIoTCoreDeviceShadow]]<HTML></p></HTML>
<code>
POST  HTTP/1.1
Host: api.ucloud.cn
Content-Type: application/json
Body:
{
 "Action": "UpdateUIoTCoreDeviceShadow",
 "ProductSN": "qn4hvcjiyqt2069t",
 "DeviceSN":"4ythk4cav6ph4310",
 "Desired": "eyJjb2xvciI6ImdyZWVuIn0=", //base64Encode({"color":"green"})
 "ShadowVersion": 1,
 "ProjectId": "org-z44lmf12e",
 "PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
 "Region": "cn-sh2",
 "Signature": "kwe6b4r35dc41b432s2d059f602047fd51c2881z"
}

</code>
<HTML><p></HTML>{{../images/设置期望.png|设置期望}}<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>在MQTT.fx操作界面可以看到下发消息；<HTML></p></HTML>
<HTML><p></HTML>{{../images/设备影子下发消息.png|设备影子下发消息}}<HTML></p></HTML><HTML></li></HTML><HTML></ol></HTML>

===== 通过自定义Topic =====

自定义Topic的具体详情参考[[|用户自定义Topic]]，创建上行和下行两个自定义Topic为：

^Topic                                      ^权限^描述  ^
|/qn4hvcjiyqt2069t/4ythk4cav6ph4310/uplink  |发布|上行消息|
|/qn4hvcjiyqt2069t/4ythk4cav6ph4310/downlink|订阅|下行消息|

==== 上行测试 ====

<HTML><ol></HTML>
<HTML><li></HTML><HTML><p></HTML>在MQTT.fx操作界面，点击<html><Publish></html>，输入Topic：''%%/qn4hvcjiyqt2069t/4ythk4cav6ph4310/uplink%%''；<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>输入任意内容的Payload：<HTML></p></HTML>
<code>
{
  "payload":"uplink-test"
}

</code><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>在日志里面查看上报成功结果，如图：<HTML></p></HTML>
<HTML><p></HTML>{{../images/自定义上行.png|自定义上行}}<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>也可以通过规则引擎M2M、HTTP、MQ等进行消息的接收消费。<HTML></p></HTML><HTML></li></HTML><HTML></ol></HTML>

==== 下行测试 ====

<HTML><ol></HTML>
<HTML><li></HTML><HTML><p></HTML>在MQTT.fx操作界面，点击<html><Subscribe></html>，输入Topic：''%%/qn4hvcjiyqt2069t/4ythk4cav6ph4310/downlink%%''；<HTML></p></HTML>
<HTML><p></HTML>{{../images/下行订阅.png|下行订阅}}<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>使用云端API进行调用，参考[[|PublishUIoTCoreMQTTMessage]]发送下行消息。 UCloud API的调用可以通过GET或POST请求，这里以POST为例，参数中密钥、签名的使用参考[[|关于API接入]]，其他参数参考[[|PublishUIoTCoreMQTTMessage]]<HTML></p></HTML>
<code>
POST  HTTP/1.1
Host: api.ucloud.cn
Content-Type: application/json
Body:
{
    "Action": "PublishUIoTCoreMQTTMessage",
    "ProductSN": "qn4hvcjiyqt2069t",
    "MessageContent": "eyJwYXlsb2FkIjoiZG93bmxpbmstdGVzdCJ9", //base64Encode({"payload":"downlink-test"})
    "TopicFullName": "/qn4hvcjiyqt2069t/4ythk4cav6ph4310/downlink",
    "ProjectId": "org-z44lmf12e",
    "PublicKey": "CJf+LfjjXPk70z/fsBlK9sHC+kBTTj7gr2g/C/R7YSi3EFTK   Cmh7Bp5W1UH64D/O",
    "Region": "cn-sh2",
    "Signature": "2we34r35dc41b434s2d059f642047fd51c2881f"
}

</code><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>在MQTT.fx操作界面看到下发消息；<HTML></p></HTML>
<HTML><p></HTML>{{../images/自定义下行.png|自定义下行}}<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>也可以通过日志查看下发成功结果<HTML></p></HTML>
<HTML><p></HTML>{{../images/自定义下行日志.png|自定义下行日志}}<HTML></p></HTML><HTML></li></HTML><HTML></ol></HTML>

