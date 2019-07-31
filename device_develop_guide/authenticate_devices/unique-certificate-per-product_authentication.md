{{indexmenu_n>3}}

# 动态注册

动态注册也叫做一型一密，也就是说同一个产品下的设备激活时使用产品公共的凭证（**产品序列号**，**产品密码**）。 然后物联网平台给设备下发**设备密码**，设备保存**设备密码**，然后使用拿到的密码按照静态注册的流程完成激活认证。      

## 操作步骤：

1\. 参考云平台操作指南，[创建产品](../../console_guide/product_device/create_products)，动态注册，打开<[动态注册](../../console_guide/product_device/create_products#产品详情)>开关；

2\. 准备工作：

   1. 开发设备端固件，使用[SDK动态注册](#动态注册)开发相应的固件；

   2. 确认产品详情页的<动态注册>开关已经打开；

   3. 参考[手动输入](../../console_guide/product_device/create_devcies#创建单个或多个设备)，在控制台批量添加即将要激活的设备序列号，以便于设备激活时进行预认证，设备进行预认证时，只有被添加过的设备才能通过云平台校验，完成预认证；

      **预认证**是指为了防止设备被仿制或冒充接入平台，需要先将表征设备的唯一标识，比如MAC、IEMI或SN等作为设备序列号预先添加到平台，这样不在该白名单内的设备就无法被激活，保证可信设备的接入。

3\. 将步骤2开发的固件直接发给产线烧录；

4\. 预认证，设备首次激活时，将表征自己唯一标识的MAC等作为设备序列号，通过产品公共凭证（**产品序列号**，**产品密码**）及该**设备序列号**进行设备预认证。

5\. 预认证通过后，设备可以接入物联网平台，但是此时权限受限，不能进行消息的收发，设备需要获取**设备密码**，通过**设备密码**登录，才能正常使用平台功能，进行消息收发。

**设备获取设备密码方法为：**

    1. 设备向Topic**/$system/${ProductSN}/${DeviceSN}/password**发送一条请求获取密码消息(RequestID任意指定)：

```
{
  "RequestID": "100"
}
```

    2. 云平台收到请求后会将**设备密码**通过Topic **/$system/${ProductSN}/${DeviceSN}/password_reply**下发给设备，消息格式为：

```
{
  "RetCode": "0", 
  "RequestID": "100",
  "Password": "the device secret"
}
```

6\. 设备通过收到的**设备密码**，以[静态注册](unique-certificate-per-device_authentication)的方式完成激活认证。



![动态注册](../../images/动态注册.png)

![](../../images/手动生成.png)

## 具体流程：

生成动态MQTT Broker认证需要的三要素：**ClientID**，**UserName**，**Password**。

1\. 获取到产品的公共凭证（**产品序列号**，**产品密码**），分别表示为**${ProductSN}**，**${ProdSecret}**；

2\. 手动添加设备序列号**${DeviceSN}**到云平台，作为允许动态注册的设备白名单；

3\. 设备将自己的某唯一标识作为**${DeviceSN}**，比如可以选取设备的MAC地址、IMEI或者SN等作为**${DeviceSN}**。

4\. 通过以下规则生成MQTTBroker认证的三要素连接云平台；

|MQTT认证三要素| 生成规则|
|---|---|
|ClientID | ${ProductSN}.${DeviceSN} 举例：70ly1tvowt696r15.112233445566|
|UserName | ```${ProductSN}|${DeviceSN}|${authmode}```  ```举例：70ly1tvowt696r15|112233445566|2``` authmode: 1 表示静态注册；2表示动态注册|
|Password | ${ProdSecret}  举例：sqx0cltqba402z7z|

5\. 预认证成功后，订阅Topic **/$system/${ProductSN}/${DeviceSN}/password_reply**，举例：**/$system/70ly1tvowt696r15/112233445566/password_reply**；

6\. 发送请求获取密码消息

```
Publish /$system/${ProductSN}/${DeviceSN}/password
举例： /$system/70ly1tvowt696r15/112233445566/password

{
  "RequestID": "100"
}
```

云平台将**设备密码**通过步骤5订阅的Topic下发，举例收到的**设备密码**为**zlc3d21u5k8fq0d2**；

```
Subscribe /$system/${ProductSN}/${DeviceSN}/password_reply
举例： /$system/70ly1tvowt696r15/112233445566/password_reply

{
  "RetCode": "0", 
  "RequestID": "100",
  "Password": "zlc3d21u5k8fq0d2"
}
```

7\. 通过静态注册的规则生成新的MQTTBroker认证的三要素：

|MQTT认证三要素|生成规则|
|---|---|
|ClientID | ${ProductSN}.${DeviceSN} 举例：70ly1tvowt696r15.112233445566|
|UserName | ```${ProductSN}|${DeviceSN}|${authmode}``` ```70ly1tvowt696r15|112233445566|1``` authmode: 1 表示静态注册；2表示动态注册|
|Password | ${DevSecret} 举例：zlc3d21u5k8fq0d2|

8\. 参考[下一节设备连接](../connecting_devices)将设备接入到物联网平台，完成认证；
