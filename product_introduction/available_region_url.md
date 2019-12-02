# 已开通区域及域名列表


目前UCloud物联网通信云平台还处于公测阶段，暂时只开通上海二，其他可用区会在2020年陆续开放，请持续关注UIoT-Core。


## 已开通可用区列表

UCloud目前拥有25大地域（Region），具体参见参见 [地域和可用区列表](https://docs.ucloud.cn/api/summary/regionlist)。 用户选择开通UIoT-Core时选择的地域，通过UIoT-Core规则引擎只能流转到同一地域的UHost、UDB、UTSDB、UKafka、UAI、USMS等产品。每个地域下开设有多个可用区（Zone），可用区与可用区之间是可以相通的，每个地域所提供的服务有所不同，用户需根据自己的实际情况选择开通的地域。

用户可以在控制台查看当前的Region，或者通过API接口[GetRegion](https://docs.ucloud.cn/api/summary/regionlist?id=getregion) 获取当前的Region。

|地域名称|地域短ID|下属可用区|
|----|----|----|
|上海二|cn-sh2|上海二可用区A、上海二可用区B、上海二可用区C|


## 涉及域名列表

下表中列出了平台的涉及的所有域名的列表，用户根据自己使用到的功能使用相应的域名。

TLS根证书分为两种：
- 自签名根证书，一般设备端接入MQTT使用，有效期20年，MQTT over TCP使用该证书；
- 国际授信根证书，不需要另外导入证书，浏览器可以直接支持，有效期10年；


|功能|域名|端口(明文/加密)|TLS根证书|
|----|----|----|----|
|[MQTT连接](/iot/uiot-core/device_develop_guide/deviceconnect/mqttconnect)|mqtt-$\{RegionId\}.iot.ucloud.cn |`1883`/`8883(使用TLS)`|[下载CA证书(自签名)](http://uiot.cn-sh2.ufileos.com/ca-cert.pem)|
|[WebSocket连接](/iot/uiot-core/device_develop_guide/deviceconnect/websocketconnect)|mqtt-$\{RegionId\}.ucloud.cn|`80`/`443(使用TLS)`|[下载CA证书(国际授信)](http://uiot.cn-sh2.ufileos.com/iot_ca.crt)|
|[HTTP连接](/iot/uiot-core/device_develop_guide/deviceconnect/httpconnect)|http-$\{RegionId\}.iot.ucloud.cn|仅支持`443(使用TLS)`|[下载CA证书(国际授信)](http://uiot.cn-sh2.ufileos.com/iot_ca.crt)|
|[云端API调用](/iot/uiot-core/api_guide/api_guidehelp)|api-$\{RegionId\}.iot.ucloud.cn|仅支持`443(使用TLS)`|[下载CA证书(国际授信)](http://uiot.cn-sh2.ufileos.com/iot_ca.crt)|
|[上传文件](/iot/uiot-core/device_develop_guide/uploadfile)|file-$\{RegionId\}.iot.ucloud.cn|仅支持`443(使用TLS)`|[下载CA证书(国际授信)](http://uiot.cn-sh2.ufileos.com/iot_ca.crt)|

