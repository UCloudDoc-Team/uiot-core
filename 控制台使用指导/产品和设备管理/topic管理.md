{{indexmenu_n>3}}
### 主题Topic
主题或者叫做Topic是物联网的平台的核心概念，也是一切消息流转的载体，平台为每个产品提供了一些默认的系统Topic，同时用户也可以针对不同的产品自定义自己的Topic，为Topic指定相应的权限。

Topic是跟随着产品一起定义的，在定义Topic时，路径中会使用`${DeviceSN}`抽象出属于产品的的Topic，当具体设备发布或订阅该Topic时，直接使用该设备的`设备序列号`来替换即可。

比如：
1. 定义某个产品的Topic为：`/7y94syp89zig70fi/${DeviceSN}/download`，具有订阅权限；
2. 某个设备的`设备序列号`为`pcur1q7jm2lb57rk`，则该设备订阅时使用Topic：`/7y94syp89zig70fi/pcur1q7jm2lb57rk/download`；



<br>
关于Topic的一些限制：   

- Topic不可以跨越产品进行发布或者订阅；
- Topic命名以正斜线`/`做层级处理，`${ProductSN}`为抽象层级，表示`产品ID`；`${DeviceSN}`为抽象层级，表示`设备序列号`；`$broadcast`Œ为抽象层级，表示某个产品下的所有`设备序列号`；
- Topic的命名只能必须由字母、数字、下划线`_`、正斜线`/`组成，不应出现两个连续的正斜线`//`；
- Topic的权限可以设置为发布、订阅、同时支持发布和订阅；
- 用户不能自定义含有系统Topic关键字的Topic，==用户自定义的topic我们是不是已经定死了？？？==；
- Topic支持MQTT默认的通配符`+`，`#`，参考[Topic通配符]()；

#### 系统Topic
系统Topic是指系统预定义的有特殊用途的Topic，比如操作[设备影子]()、操作[物模型]()、操作设备状态、操作[固件升级]()，具体概念可以参考对应章节。

系统Topic会在第一层级以`/$xxxx`开始，自定义Topic需要避免这些关键字。

Topic | 权限|描述
|---|---|---
|/$shadow/upstream/${ProductSN}/${DeviceSN} |发布|更新设备影子
|/$shadow/downstream/${ProductSN}/${DeviceSN} | 订阅| 设置期望值
|/$system/${ProductSN}/${DeviceSN}/rpc/request/message_id|订阅| rpc调用
|/$system/${ProductSN}/${DeviceSN}/rpc/response/message_id|发布|响应rpc调用
|/$system/${ProductSN}/${DeviceSN}/status|订阅|设备状态
|/$system/${ProductSN}/${DeviceSN}/property/set|订阅|设置属性
|/$system/${ProductSN}/${DeviceSN}/property/post|发布|设备上报属性，以及响应设置属性
|/$system/${ProductSN}/${DeviceSN}/property/restore|发布|请求恢复属性值
|/$system/${ProductSN}/${DeviceSN}/property/restore_reply|订阅|云平台回复回复属性值
|/$system/${ProductSN}/${DeviceSN}/property/latest|订阅|云平台推送物模型最新属性值
|/$system/${ProductSN}/${DeviceSN}/event/post|发布|设备上报事件
|/$system/${ProductSN}/${DeviceSN}/tmodel/get|发布|设备请求获取物模型
|/$system/${ProductSN}/${DeviceSN}/tmodel/get_reply|订阅|云平台回复获取物模型请求
|/$ota/upstream/${ProductSN}/${DeviceSN}|发布|设备上报固件版本升级状态
|/$ota/downstream/${ProductSN}/${DeviceSN}|订阅|云端下发固件升级消息


#### 用户自定义Topic
用户可以通过<主题管理>添加自定义Topic，并指定这些Topic的发布或订阅权限。

##### 操作步骤
1. [注册](https://passport.ucloud.cn/#register)UCloud云服务，如已注册请直接第2步；
2. 登录进入UCloud[物联网平台](https://console.ucloud.cn/iot)；
3. 选择<产品管理>标签；
4. 选中需要定义Topic的产品，进入产品详情页；
5. 点击<主题管理>标签，点击<定义Topic类>，添加Topic；
6. - 设置Topic类：
     - 输入Topic的剩余层级内容；
     - 选择Topic权限，发布或者订阅；
     - 输入描述；
     - 单击<确定>，创建成功；
   - 设置<接收广播Topic(${DeviceSN})>
     - 输入Topic的剩余层级内容；
     - 输入描述
     - 单击<确定>，创建成功；

<img src="https://ushare.ucloudadmin.com/download/attachments/12793734/%E6%B7%BB%E5%8A%A0topic%E7%B1%BB.png?version=1&modificationDate=1557197062865&api=v2" width="900" />

##### 自定义Topic的删除
1. 接上述操作步骤，仍然在<主题管理>标签；
2. 点击<删除>，点击<确定>，删除成功；

自定义Topic删除注意事项：
- 自定义Topic具有发布权限，平台将不再接收该Topic的数据；
- 自定义Topic具有订阅权限，设备将无法订阅该Topic，已经订阅的设备将不再能收到数据；
- 自定义Topic删除后，规则引擎的Topic需要自行删除，规则引擎不做Topic的有效性的校验；


<img src="https://ushare.ucloudadmin.com/download/attachments/12793734/%E5%88%A0%E9%99%A4topic.png?version=1&modificationDate=1557197061710&api=v2" width="900" />

##### 广播Topic
广播Topic是指某个产品公用的Topic，只具有订阅权限，所有该产品下的设备均可以订阅该Topic。云应用可以通过API发送数据到该Topic，所有订阅了该Topic的设备都会收到该数据。


假如一个Topic只有订阅权限，那就意味着这个Topic只有平台可以发布消息。那这样的Topic规则引擎可以转到哪里？
那规则引擎里面可以将一个只有订阅权限的Topic转发给只有发布权限的Topic吗？

#### Topic通配符
设备可以订阅或发布含有通配符的Topic(仅限于用户自定义部分层级)，在规则引擎中，也可以使用通配符做数据转发的设置。


|通配符 |	描述
|---|---
|# |	这个通配符必须出现在Topic的最后一个层级，代表本级及下级所有类目。例如， Topic /7y94syp89zig70fi/pcur1q7jm2lb57rk/upload/#中，/upload层级后使用通配符#，代表/download层级后的所有层级。该Topic可以代表/7y94syp89zig70fi/pcur1q7jm2lb57rk/upload/data和/7y94syp89zig70fi/pcur1q7jm2lb57rk/upload//error。
|+ |	代表本级所有符合的。例如，Topic /7y94syp89zig70fi/+/upload中，代表产品下所有设备，可以代表/7y94syp89zig70fi/deviceA/upload和/7y94syp89zig70fi/deviceB/upload。
