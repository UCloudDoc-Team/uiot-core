{{indexmenu_n>1}}
### 规则引擎概览
物联网平台除了提供产品管理、设备管理还提供基于Topic的数据流管理。无论是设备端的数据或者用户端的数据，只要是基于Topic的数据上报都可以通过规则引擎进行数据的流转，从而转发到UCloud平台的其他产品。用户在不需要自己搭建基础设备的情况下直接消费数据，完成自身的业务逻辑。

平台支持数据流转的方式有：
- 数据流转到MongoDB中；
- 数据流转到TSDB中；
- 数据流转到分布式消息系统Kafka中；
- 数据流转到其他Topic，实现M2M；
- 数据流转到短信平台；



#### 操作步骤：
1. [注册](https://passport.ucloud.cn/#register)UCloud云服务，如已注册请直接第2步；
2. 登录进入UCloud[物联网平台](https://console.ucloud.cn/iot)；
3. 选择<规则引擎>标签；
4. 点击<新建规则>，输入规则名称及描述；
5. 点击<确定>，创建规则成功；

<img src="https://ushare.ucloudadmin.com/download/attachments/14746235/%E6%96%B0%E5%BB%BA%E8%A7%84%E5%88%99.png?version=1&modificationDate=1557288460442&api=v2" width="900" />

#### 规则启用
规则启用指的是让规则生效开始运行，规则创建之后不能立即启用，还需要对规则做[数据流转设置]()才可以<启用>。

<启用>之后可以通过<禁用>使规则暂不生效。


#### 规则删除
规则的删除支持单个删除和批量删除。

规则删除注意事项：
- 启用的规则需要先禁用再删除；
- 规则删除后将无法找回，如需创建需要重新创建；
- 规则删除立即生效；

<img src="https://ushare.ucloudadmin.com/download/attachments/14746235/%E7%A6%81%E7%94%A8%E5%88%A0%E9%99%A4.png?version=1&modificationDate=1557288460257&api=v2" width="900" />

#### 规则建立
下一节将介绍如何为规则创建具体的流转配置。




### SQL表达式特性
SQL表达式可以很灵活的筛选出想要的消息内容并发往不同的目的地。

```
例如某个产品7y94syp89zig70fi下的某个设备上报的数据格式为：
{
	"temperature": 25.1,
	"humidity": 65
}

假定温度大于38，湿度小于40时的数据需要流转到其他服务做保存或处理，可以编写如下的SQL语句：
SELECT temperature as t, deviceSN() as deviceSN FROM /7y94syp89zig70fi/+/update WHERE temperature > 38 and humidity < 40
对于该产品下的所有数据（+表示通配所有设备），当温度大于38且湿度小于40时，会触发该规则，并且解析数据中的温度、设备序列号，然后流转到目的地。
```

#### SELECT
Select支持以下类型：
- [内置函数]()，比如`deviceSN()`；
- JSON属性表达式，比如`light.state`；
- 星号`*`，表示所有内容；
- JSON第一层key，比如`temperature`；


#### FROM
From值需要筛选的Topic，支持通配符，参考[Topic]()。

##### Topic通配符
在规则引擎中，通配符可以匹配一类Topic做数据转发的设置。


|通配符 |	描述
|---|---
|# |	这个通配符必须出现在Topic的最后一个层级，代表本级及下级所有类目。例如， Topic /7y94syp89zig70fi/pcur1q7jm2lb57rk/upload/#中，/upload层级后使用通配符#，代表/download层级后的所有层级。该Topic可以代表/7y94syp89zig70fi/pcur1q7jm2lb57rk/upload/data和/7y94syp89zig70fi/pcur1q7jm2lb57rk/upload//error。
|+ |	代表本级所有符合的。例如，Topic /7y94syp89zig70fi/+/upload中，代表产品下所有设备，可以代表/7y94syp89zig70fi/deviceA/upload和/7y94syp89zig70fi/deviceB/upload。

#### WHERE
Where表示条件，支持以下语法：

- 比较运算符
  - \>   大于
  - <    小于
  - \>=  大于等于
  - <=   小于等于
  - =    等于
  - <>   不等于
  
- 逻辑运算符
  - and  与
  - or   或
  
- 括号运算符 ()
- 算术运算符
  - \+
  - \-
  - \*
  - /
  - %
- [函数调用]()
- JSON属性表达式
- CASE 语句
- IN
- LIKE


#### 类型转换
字符串和数字进行比较等操作时的类型互转。？？？？ 
==算数和比较运算符有类型提升，两种类型运算由低类型往高类型转==


#### 函数列表
SQL表达式可以使用函数来优化我们的SQL语句，使得消息筛选更加灵活。

函数可以在SELECT或者WHERE中使用。

| 函数名|	函数说明|
|---|---|
|abs(number)	|返回绝对值。
|asin(number)	|返回number值的反正弦。
|concat(string1, string2)	|字符串连接  <br>示例：concat(field,’a’)
|cos(number)	|返回number值的余弦。
|cosh(number)	|返回number值的双曲余弦（hyperbolic cosine）。
|deviceSN()	    |返回当前设备序列号
|endswith(input, suffix)	|判断input值是否以suffix结尾。
|exp(number)	|返回指定数字的指定次幂。
|floor(number)	|返回一个最接近它的整数，它的值小于或等于这个浮点数。
|lower(string)	|返回小写字符串。
|rand()	|返回[0~1)之间随机数。
|replace(source, substring, replacement)|对某个目标列值进行替换。<br>示例：replace(field,’a’,’1’)。
|sin(n)	    |返回n值的正弦。
|sinh(n)	|返回n值的双曲正弦（hyperbolic sine）。
|tan(n)	    |返回n值的正切。
|tanh(n)	|返回n值的双曲正切（hyperbolic tangent）。
|topic(number)	 |返回Topic分段信息。<br>如，有一个Topic： /abcdef/ghi。使用函数 topic()，则 返回 “/abcdef/ghi”； 使用 topic(1)，则 返回 “abcdef” ； 使用 topic(2) |，则返回 “ghi”。
|upper(string)	|返回大写字符。

