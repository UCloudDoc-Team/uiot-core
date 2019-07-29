{{indexmenu_n>6}}

====== 设备OTA升级 ======

OTA（Over-the-Air Technology）即空中下载技术。在设备端开发中可以理解为固件升级技术。用户可以基于物联网平台的OTA技术直接进行OTA升级、应用配置远程更新下发等操作。

===== 固件升级Topic =====

固件升级的过程中涉及两个Topic：

^Topic                                           ^权限^描述               ^
|/$system/${productSN}/${deviceSN}/ota/upstream  |发布|设备上报固件版本及下载、升级状态 |
|/$system/${productSN}/${deviceSN}/ota/downstream|订阅|设备接收应用服务下发的固件升级消息|

{{../images/框图.jpg|框图}}

===== 具体流程 =====

设备的升级流程如下所示：

{{../images/流程图.jpg|流程图}}

<HTML><ol></HTML>
<HTML><li></HTML><HTML><p></HTML>设备上报版本号；<HTML></p></HTML>
<HTML><p></HTML>设备端向''%%/$system/${productSN}/${deviceSN}/ota/upstream%%''发布一条消息进行版本上报，消息格式如下：<HTML></p></HTML>
<code>
{
    "method": "report_version",
    "payload":{
        "version": "1.0"
    }
}

</code>
<HTML><p></HTML>参数解释:<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>method：消息类型为report_version<HTML></li></HTML>
<HTML><li></HTML>version：上报的版本号<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>用户在控制台[[|新增固件]]或调用接口[[|GetUIoTCoreUploadURL]]获取上传固件地址进行固件上传；<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>用户通过控制台发起[[|固件升级请求]]或调用接口[[|UpdateUIoTCoreDeviceFW-更新单个设备]]/[[|BatchUpdateUIoTCoreDeviceFW-批量升级设备]]；<HTML></p></HTML><HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>云端下发固件升级消息给设备端 设备端会通过订阅的''%%/$system/${productSN}/${deviceSN}/ota/downstream%%''收到固件升级的消息，内容如下：<HTML></p></HTML>
<code>
{
    "method": "update_firmware",
    "payload":{
        "version": "2.0",
        "url": "http://uiottestufile.cn-sh2.ufileos.com",
        "md5": "aa30e838c7cdbbcbf8be7668aaeebee3",
        "size": 10000
    }
}

</code>
<HTML><p></HTML>参数解释：<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>method：消息类型为update_firmware<HTML></li></HTML>
<HTML><li></HTML>version：升级版本<HTML></li></HTML>
<HTML><li></HTML>url：下载固件的url<HTML></li></HTML>
<HTML><li></HTML>md5：固件的MD5值<HTML></li></HTML>
<HTML><li></HTML>size：固件大小，单位为字节<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>设备在收到固件升级的消息后，根据URL下载固件，通过''%%/$system/${productSN}/${deviceSN}/ota/upstream%%''上报下载进度，消息格式如下：<HTML></p></HTML>
<code>
{
    "method": "report_progress",
    "payload":{
        "state":"downloading",
        "percent": 50
    }
}

</code>
<HTML><p></HTML>参数解释：<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>method：消息类型为report_progress<HTML></li></HTML>
<HTML><li></HTML>state：状态为正在下载中<HTML></li></HTML>
<HTML><li></HTML>percent：当前下载进度，百分比<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>当设备下载完固件，通过''%%/$system/${productSN}/${deviceSN}/ota/upstream%%''上报升级进度，消息格式如下：<HTML></p></HTML>
<code>
{
    "method": "report_progress",
    "payload":{
        "state":"burning",
        "percent": 50
    }
}

</code>
<HTML><p></HTML>参数解释：<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>method：消息类型为report_progress<HTML></li></HTML>
<HTML><li></HTML>state：状态为固件烧录中<HTML></li></HTML>
<HTML><li></HTML>percent：当前烧录进度，百分比<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>设备固件升级完成后，通过''%%/$system/${productSN}/${deviceSN}/ota/upstream%%''上报升级成功消息，消息格式如下：<HTML></p></HTML>
<code>
{
    "method": "report_success",
    "payload":{
        "version": "2.0"
    }
}

</code>
<HTML><p></HTML>参数解释：<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>method：消息类型为report_success<HTML></li></HTML>
<HTML><li></HTML>version：当前固件版本，注意升级成功消息的version字段一定要与目标版本相符，否则云端会按升级失败处理<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML>
<HTML><li></HTML><HTML><p></HTML>若升级失败，通过''%%/$system/${productSN}/${deviceSN}/ota/upstream%%''上报升级失败消息，消息格式如下：<HTML></p></HTML>
<code>
{
    "method": "report_fail",
    "payload":{
        "err_code": -1,
    }
}

</code>
<HTML><p></HTML>参数解释：<HTML></p></HTML>
<HTML><ul></HTML>
<HTML><li></HTML>method：消息类型为report_fail<HTML></li></HTML>
<HTML><li></HTML>err_code：错误码，
<HTML><ul></HTML>
<HTML><li></HTML>-1：URL无法访问；<HTML></li></HTML>
<HTML><li></HTML>-2：URL签名过期；<HTML></li></HTML>
<HTML><li></HTML>-3：下载超时；<HTML></li></HTML>
<HTML><li></HTML>-4: MD5不匹配；<HTML></li></HTML>
<HTML><li></HTML>-5：固件烧录失败<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML><HTML></ul></HTML>
<HTML></li></HTML><HTML></ol></HTML>

**离线处理：**\\
设备离线时，不能接收服务端推送的升级消息。通过当设备再次上线后，主动请求固件更新消息。OTA服务端收到设备上线消息，验证该设备是否需要升级。如果需要升级，再次推送升级消息给设备， 否则，不推送消息。

请求固件更新消息格式：

<code>
    {
        "method": "request_firmware",
        "payload":{
            "version": "0.1"
        }
    }


</code>
参数解释：

  * method：消息类型为request_firmware
  * version：当前固件版本，如果有固件升级信息，服务器会推送，否则不推送

