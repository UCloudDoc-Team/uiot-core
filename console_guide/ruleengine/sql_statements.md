# SQL表达式特性
SQL表达式可以很灵活的筛选出想要的消息内容并发往不同的目的地。

```
例如某个产品70ly1tvowt696r15下的某个设备上报的数据格式为：
{
	"temperature": 25,
	"humidity": 65
}

假定温度大于30，湿度小于50时的数据需要流转到其他服务做保存或处理，可以编写如下的SQL语句：
SELECT temperature as t, deviceSN() as deviceSN FROM /70ly1tvowt696r15/+/upload WHERE temperature > 30 and humidity < 50
对于该产品下的所有数据（+表示通配所有设备），当温度大于30且湿度小于50时，会触发该规则，并且解析数据中的温度、设备序列号，然后流转到目的地。
```

## SELECT
JSON数据类型支持以下类型：

- 内置函数，支持函数参考[函数列表JSON](#函数列表)，比如`deviceSN()`；
- JSON属性表达式，比如`light.state`；
- 星号`*`，表示所有内容；
- 支持使用`as`对筛选的字段定义别名，比如`temperature as t`；

binary数据类型支持以下类型：

- 部分内置函数，支持函数参考[函数列表binary](#函数列表)，比如`deviceSN()`；
- 星号`*`，表示所有内容；


注：SELECT出来的新的字段将会作为JSON的一个新的字段发送到目的地，比如采用上面的例子，数据格式为JSON，规则为：

```
SELECT deviceSN(),* FROM /70ly1tvowt696r15/+/upload
```
则结果为
```
{
	"deviceSN()": "00:14:32:e1:72:f1",
	"temperature": 25,
	"humidity":65
	
}
```
在定义规则引擎的执行动作存储到结构化存储时，则使用`${deviceSN()}`和`${temperature}`、`${humidity}`配置字段值。


## FROM
From值需要筛选的Topic，支持通配符，参考[Topic管理](../product_device/topic)。

binary数据类型仅支持自定义Topic，不支持系统Topic。

### Topic通配符
在规则引擎中，通配符可以匹配一类Topic做数据转发的设置。


|通配符 |	描述
|---|---
|# |	**这个通配符必须出现在Topic的最后一个层级，代表本级及下级所有类目。**<br>例如， Topic /70ly1tvowt696r15/pcur1q7jm2lb57rk/upload/#中，/upload层级后使用通配符#，代表/download层级后的所有层级。该Topic可以代表/70ly1tvowt696r15/pcur1q7jm2lb57rk/upload/data和/70ly1tvowt696r15/pcur1q7jm2lb57rk/upload//error。
|+ |	**代表本级所有符合的。**<br>例如，Topic /70ly1tvowt696r15/+/upload中，代表产品下所有设备，可以代表/70ly1tvowt696r15/deviceA/upload和/70ly1tvowt696r15/deviceB/upload。

## WHERE
JSON数据类型支持以下类型：

- 内置函数，支持函数参考[函数列表-JSON](#函数列表)，比如`deviceSN()`；
- JSON属性表达式的条件语句，比如`light.state = 0`；
- 留空，所有数据；

binary数据类型支持以下类型：

- 部分内置函数，支持函数参考[函数列表-binary](#函数列表)，比如`deviceSN()`；
- 内置函数的条件表达式；

### WHERE 条件语法
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
- [函数调用](#函数列表)
- JSON属性表达式
- CASE 语句
- IN
- LIKE


## 类型转换

字符串和数字进行比较等操作时的类型互转时，两种类型运算由低类型往高类型转。

比如`int32`和`int64`比较时，转变为`int64`和`int64`比较；`int32`和`string`比较时，转变为`string`和`string`比较。


## 函数列表
SQL表达式可以使用函数来优化我们的SQL语句，使得消息筛选更加灵活。

函数可以在SELECT或者WHERE中使用。

| 函数名|	函数说明|JSON |binary|
|---|---|---|---|
|abs(number)	|返回绝对值。|√|×|
|asin(number)	|返回number值的反正弦。|√|×|
|concat(string1, string2)	|字符串连接  <br>示例：concat(field,’a’)。|√|√|
|cos(number)	|返回number值的余弦。|√|×|
|cosh(number)	|返回number值的双曲余弦（hyperbolic cosine）。|√|×|
|deviceSN()	    |返回当前设备序列号。|√|√|
|endswith(input, suffix)	|判断input值是否以suffix结尾。|√|×|
|exp(number)	|返回指定数字的指定次幂。|√|×|
|floor(number)	|返回一个最接近它的整数，它的值小于或等于这个浮点数。|√|×|
|lower(string)	|返回小写字符串。|√|√|
|rand()	|返回[0~1)之间随机数。|√|√|
|replace(source, substring, replacement)|对某个目标列值进行替换。<br>示例：replace(field,’a’,’1’)。|√|√|
|sin(n)	    |返回n值的正弦。|√|×|
|sinh(n)	|返回n值的双曲正弦（hyperbolic sine）。|√|×|
|tan(n)	    |返回n值的正切。|√|×|
|tanh(n)	|返回n值的双曲正切（hyperbolic tangent）。|√|×|
|topic(number)	 |返回Topic分段信息。<br>如，有一个Topic： /abcdef/ghi。使用函数 topic()，则 返回 "/abcdef/ghi"； 使用 topic(1)，则 返回 "abcdef" ； 使用 topic(2) ，则返回 "ghi"。|√|√|
|upper(string)	|返回大写字符。|√|√|
|to_base64()|当原始Payload数据为二进制数据时，可使用该函数，将所有二进制数据转换成base64String。|√|√|