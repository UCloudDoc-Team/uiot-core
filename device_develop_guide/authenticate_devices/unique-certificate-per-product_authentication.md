# 动态注册

动态注册也叫做一型一密，一型一密是指同一个产品下的设备激活时使用产品公共的凭证（`产品序列号`，`产品密码`）进行连接，然后再获取`设备密码`。

获取到`设备密码`后，设备将`设备密码`保存到不易失存储中，然后使用取得的`设备密码`按照[静态注册](unique-certificate-per-device_authentication)的流程完成动态激活认证。 


注：设备通过动态注册获取到设备密码登录成功一次后，将不能再进行动态注册，否则将出现权限受限。    



## 操作步骤：

1. 参考云平台操作指南，[创建产品](../../console_guide/product_device/create_products)，打开<动态注册>开关；

2. 参考[产品详情页](../../console_guide/product_device/create_products#产品详情)，打开或关闭<预认证>开关；

      #### 预认证  
	  
	  是指为了防止设备被仿制或冒充接入平台，先将表征设备的唯一标识，比如MAC、IEMI或SN等作为设备序列号预先通过手动添加设备的方式批量添加到平台，这样不在该白名单内的设备就无法被激活，保证可信设备的接入。
	  
	  预认证可以关闭，关闭即是指动态注册时，不对设备号进行校验。
	  


3. 准备工作：

   1). 开发设备端固件，比如使用[C-SDK动态注册](../../device_develop_guide/c_sdk_example/mqttinterface#动态认证)开发相应的固件；
   
   2). 确认产品详情页的<动态注册>开关已经打开；
   
   3). 如果预认证打开（关闭则忽略该条）：参考[创建单个或多个设备-手动输入](../../console_guide/product_device/create_devcies#创建单个或多个设备)，在控制台批量添加即将要激活的设备序列号，以便于设备激活时进行预认证，设备进行预认证时，只有被添加过的设备才能通过云平台校验，完成预认证；

   
4. 将步骤2开发的固件直接发给产线烧录；

5. 设备首次激活时，将表征自己唯一标识的MAC等作为`设备序列号`，通过产品公共凭证（`产品序列号`，`产品密码`）及该`设备序列号`进行设备注册。如果预认证开关打开，则要确保该设备序列号已经手动添加到IoT-Core平台。

6. 预认证通过后（如果打开该开关），设备可以接入物联网平台，但是此时权限受限，不能进行消息的收发，设备需要获取`设备密码`，通过`设备密码`登录，才能正常使用平台功能，进行消息收发。

**设备获取`设备密码`方法为：**

   设备向Topic`/$system/${ProductSN}/${DeviceSN}/password`发送一条请求获取密码消息(RequestID任意指定)：

   ```
   {
   	"RequestID": "100"
   }
   ```
   云平台收到请求后会将`设备密码`通过Topic `/$system/${ProductSN}/${DeviceSN}/password_reply`下发给设备，消息格式为：
   ```
   {
    "RetCode": "0", 
   	"RequestID": "100",
   	"Password": "the device secret"
   }
   ```

7. 设备通过收到的`设备密码`，以[静态注册](../../device_develop_guide/authenticate_devices/unique-certificate-per-device_authentication)的方式完成激活认证。



![动态注册](../../images/动态注册.png)

![手动输入](../../images/手动生成.png)



## 具体流程：

生成动态MQTT Broker认证需要的三要素：`ClientID`，`UserName`，`Password`。
1. 获取到产品的公共凭证（`产品序列号`，`产品密码`），分别表示为`${ProductSN}`，`${ProdSecret}`；

2. 如果预认证开关打开，手动添加设备序列号`${DeviceSN}`到云平台，作为允许动态注册的设备白名单；

3. 设备将自己的某唯一标识作为`${DeviceSN}`，比如可以选取设备的MAC地址、IMEI或者SN等作为`${DeviceSN}`。

4. 通过以下规则生成MQTTBroker认证的三要素连接云平台；

MQTT认证三要素| 生成规则
---|---
ClientID | `${ProductSN}.${DeviceSN}`<br>举例：`70ly1tvowt696r15.112233445566`
UserName | `${ProductSN}\|${DeviceSN}\|${authmode}`<br>举例：`70ly1tvowt696r15\|112233445566\|2`<br>`authmode: 1 表示静态注册；2表示动态注册`
Password | `${ProdSecret}`<br>举例：`sqx0cltqba402z7z`

5. 订阅Topic `/$system/${ProductSN}/${DeviceSN}/password_reply`，举例：`/$system/70ly1tvowt696r15/112233445566/password_reply`；

6. 发送请求获取密码消息
   ```
   Publish /$system/${ProductSN}/${DeviceSN}/password
   举例： /$system/70ly1tvowt696r15/112233445566/password
   
   {
   	"RequestID": "100"
   }
   ```
   云平台将`设备密码`通过步骤5订阅的Topic下发，举例收到的`设备密码`为`zlc3d21u5k8fq0d2`；
   ```
   Subscribe /$system/${ProductSN}/${DeviceSN}/password_reply
   举例： /$system/70ly1tvowt696r15/112233445566/password_reply
   
   {
    "RetCode": "0", 
   	"RequestID": "100",
   	"Password": "zlc3d21u5k8fq0d2"
   }
   ```

7. 通过静态注册的规则生成新的MQTTBroker认证的三要素：

MQTT认证三要素| 生成规则
---|---
ClientID | `${ProductSN}.${DeviceSN}`<br>举例：`70ly1tvowt696r15.112233445566`
UserName | `${ProductSN}\|${DeviceSN}\|${authmode}`<br>举例：`70ly1tvowt696r15\|112233445566\|1`<br>`authmode: 1`表示静态注册；2表示动态注册`
Password | `${DeviceSecret}`<br>举例：`zlc3d21u5k8fq0d2`

8. 参考[下一节设备连接](../../device_develop_guide/deviceconnect)将设备接入到物联网平台，完成认证；


