# 数据流转到HTTP服务
数据流转到AI-Inference服务需要：

- 完成[数据流转管理](/iot/uiot-core/console_guide/ruleengine/data_forwarding)中操作步骤的前两步，已经配置好消息筛选SQL；
- 在UCloud创建了[UAI Inference AI在线服务](https://console.ucloud.cn/uai)，并已经提供HTTP服务；


## 操作步骤
1. 在[数据流转管理](/iot/uiot-core/console_guide/ruleengine/data_forwarding)页面中，点击<添加动作>;
2. 在弹出的对话框中，选择动作"转发到UAI在线服务"；

   - 选择动作：选择需要流转到的目的地，这里选择“转发到UAI在线服务”；
   - UAI在线服务名称：选择已经创建的UAI在线服务；
   - HTTP服务路径 ：填写UAI在线服务中提供的服务地址；
   - Token：在UAI在线服务控制台<全局用户组管理>、<管理令牌>中获取；
   
3. 填写完毕后，点击<确定>，完成动作的添加；
4. 回到规则引擎列表页，选择<启用>，规则变为运行状态；
5. 测试此条规则是否生效；


![转发到AI服务](/images/转发到AI服务.png)



