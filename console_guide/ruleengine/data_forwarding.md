# 数据流转管理
数据的流转是通过一种类似SQL语句的方式，对Topic消息内容进行筛选，将筛选的数据流转到目的地。

数据流转JSON和binary数据类型的区别：  

- JSON：JSON格式对于文档数据会先进行数据解析，提前JSON中的字段，再进行数据的流转。如果是非JSON格式的数据将会被规则引擎直接丢弃；
- binary：binary格式仅支持自定义Topic类，只做数据透传，不能流转到结构化存储的目的地中（只能流转到Kafka、M2M、HTTP、AI服务）；规则中的字段支持星号"*"，或者是部分内置函数；

## 操作步骤

1. 在上一节规则列表的页面，点击<管理>，进入数据流转管理页面;

   - **管理页面介绍**
   
     - 基本信息：规则的名称以及规则的描述和数据类型；
     - 消息筛选：编辑类似SQL语句，筛选出Topic、Topic字段；
     - 执行动作：添加动作，将消息筛选出来的数据流转到其他产品，比如UHost、MySQL、MongoDB、KafkaMQ、TSDB、M2M、AI-Inference等；
   
2. 消息筛选：  
   
   消息筛选的的规则查询语句为：`SELECT【字段】FROM【Topic】WHERE【条件】`  
   
   - Topic：分为系统Topic和自定义Topic。系统Topic是设备影子、物模型、设备状态等系统预留的Topic；自定义Topic是用户自己定义的Topic，以`/`分割，可包含字母、数字、`-`、`_`、`@`、`:`、`+`、`#`，支持五层，长度限制64，`+`和`#`为[通配符](uiot-core/console_guide/ruleengine/sql_statements#Topic通配符)，`#`只能放在结尾。具体可以根据需求选择产品，选择相应的Topic。
   - 字段：字段支持内置函数、JSON表达式、星号`*`，参考[SQL表达式特性](uiot-core/console_guide/ruleengine/sql_statements)；
   - 条件：支持比较运算符、逻辑运算符、括号运算符、算数运算符、函数调用、JSON表达式、CASE语句、IN、LIKE操作；具体参考[SQL表达式特性](uiot-core/console_guide/ruleengine/sql_statements);
   
3. 添加动作：将在[数据流转到http/kafka/mysql/TSDB/AI](uiot-core/console_guide/ruleengine/forward_data_to_mysql)中逐一介绍；

![消息筛选](/images/消息筛选.png)
![添加动作](/images/添加动作.png)
![编辑规则](/images/编辑规则.png)
