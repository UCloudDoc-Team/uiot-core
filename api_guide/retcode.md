# 返回码

### 错误码
| 错误码         | 中文                                                  | 英文                                                  |
| -------------- | ---------------------------------------------------- | --------------------------------------------------- |
|-1|数据加载失败，请稍后重试。|Data loading failed, please retry later.|
|0|请求成功|Request Success.|
|100|签名生成失败,请联系技术支持或提交工单。|Signature generation failed, please contact technical support or submit a ticket.|
|110|该操作请求超时，请稍后重试|This operation request has timed out, please retry later|
|120|日期格式错误，请重新选择日期。|Date format error, please reselect the date.|
|130|服务目前不可用，我们正在努力恢复中，请稍后重试。|Service is temporarily unavailable, we are working hard to restore it, please retry later.|
|140|权限错误，请联系技术支持或提交工单。|Authorization error, please contact technical support or submit a ticket.|
|150|服务目前不可用，我们正在努力恢复中，请稍后重试。|Service is temporarily unavailable, we are working hard to restore it, please retry later.|
|151|网关缓存服务异常|Redis Service unavilable|
|152|API 错误或后端不可用|API Error Or Service unavailable|
|160|缺少关键参数Action，请提供完整的参数。|Key parameter Action is missing, please provide the complete parameters.|
|161|Action 不存在|Action not found|
|170|缺少关键参数signature，请提供完整的参数。|Key parameter Signature is missing, please provide the complete parameters.|
|171|签名错误。|Signature error.|
|172|该账号不存在。|This account does not exist.|
|173|账户限制|Account restriction|
|174|Token 不存在|Token Not Exists|
|180|缺少关键参数API version。|Key parameter API Version is missing.|
|190|API版本错误。|API Version error.|
|200|服务目前不可用，我们正在努力修复中，请稍后再试。|Service is temporarily unavailable, we are working hard to restore, please retry later.|
|210|缺少关键参数，请提供完整的参数信息。|Key parameter is missing, please provide the complete parameters.|
|220|参数超出范围，请重新输入。|Parameter exceeds limits, please reenter.|
|230|参数错误，请重新输入。|Parameter error, please reenter.|
|240|权限错误，请联系技术支持|Authorization error, please contact technical support|
|260|降级失败,请联系技术支持或提交工单。|Downgrade failed, please contact technical support or submit a ticket.|
|270|结算错误,请联系技术支持或提交工单。|Settlement error, please contact technical support or submit a ticket.|
|290|项目未授权|project unauthorized error|
|291|该账户没有执行对应 Action 和产品类型的权限|Action , ProductType unauthorized error|
|292|项目不存在|project not exists|
|293|地区权限错误|Region Unauthorized Error|
|294|访问ip被黑名单|Access ip denied|
|295|安全锁认证失败|Safe lock miss verification|
|300|结束时间不能小于开始时间，请重新选择。|End time cannot be less than start time, please reselect.|
|310|参数类型错误|param type error|
|520|余额不足，请充值。|Balance is insufficient, please recharge.|
|999|抱歉当前机房服务目前不可用，恢复中。|Sorry, server room service is currently unavailable, restoration is in progress.|
| 100000         | 创建产品失败                                           | Create product failed                                |
| 100001         | 产品名称已存在                                          | Product name exists                                  |
| 100002         | 产品名称不存在                                          | Product name does not exists                         |
| 100003         | 产品序列号不存在                                           | Product SN does not exist                              |
| 100004         | 生成产品序列号失败                                           | Failed to generate product sn                              |
| 100005         | 产品Topic已存在                                           | Product topic exists                              |
| 100006         | 产品Topic不存在                                           | Product topic does not exist                               |
| 100007         | 设备已存在                                           | Device exists                             |
| 100008         | 设备不存在                                       | Device does not exist                             |
| 100009         | 生成设备序列号失败                                           | Generate device sn failed                             |
| 100010         | 生成设备密码失败                                           | Failed to generate device's password                             |
| 100011         | 规则名称已存在                                           | Rule name exists                              |
| 100012         | 规则ID不存在                                           | Rule ID does not exist                         |
| 100013         | 规则SQL语句不完整                                           | Rule's SQL statement is not complete                             |
| 100014         | 设备密码错误                                           | Device password is not correct                               |
| 100015         | 规则Action已存在                                           | Rule Action exists                           |
| 100016         | 规则Action不存在                                           | Rule action does not exist                        |
| 100017         | 规则Action不完整                                           | Rule Action is not complete                        |
| 100019         | 设备数超过限制                                          | Device count under product over limitation          |
| 100020         | 没有找到记录                                           | No records found                               |
| 100021         | SQL语句不合法                                           | Sql is invalid                              |
| 100022         | 该规则正在运行，修改前请先禁用                                           |Rule status is invalid                   |
| 100023         | 连接Action转发目的地失败                                           |Connect to action backend failed               |
| 100024         | 生产产品密钥失败                                           |Generate product password failed              |
| 100025         | 断开设备连接失败                                           |Failed to disconnect device               |
| 100026         | 设备影子文档版本冲突                                           |Device shadow message version conflicted           |
| 100027         | 操作关闭的设备影子                                           |Device shadow already disabled               |
| 100028         | 规则已存在                                           |Rule exist               |
| 100029         | 获取监控数据失败                                           |Get Monitor data failed               |
| 100030         | 无效的访问时间范围                                           |Invalid time range              |
| 100031         | 固件版本已存在                                         |Firmware version exist              |
| 100032         | 固件版本不存在                                         |Firmware version not exist             |
| 100033         | 设备固件版本未上报                                      |Device version is unreported              |
| 100034         | 当前版本与目标版本一致                                  |Current version equals destination version           |
| 100035         | 其他OTA任务正在运行                                         |Another OTA task is running              |
| 100036         | 设备固件版本不存在                                         |Device version not exist             |
| 100037         | 固件数量达到上限                                         |Maximum number of files exceeded              |
| 100038         | 标识符不存在                                         |Identifier not exist              |
| 100039         | 设备不在线                                         |Device is not online              |
| 100040         | 命令执行超时                                         |Command timeout              |
| 100041         | 命令回复错误                                         |Command reply error              |
| 100042         | 命令已存在                                         |Command exist              |
| 100043         | 事件已存在                                         |Event exist             |
| 100044         | 命令数量达到上限                                         |Maximum number of commands exceeded             |
| 100045         | 事件数量达到上限                                         |Maximum number of events exceeded             |
| 100046         | 命令不存在                                         |Command not exist              |
| 100047         | 事件不存在                                         |Event not exist              |
| 100048         | 属性已存在                                         |Property exist              |
| 100049         | 属性只读                                         |Read only property              |
| 100050         | 物模型属性数量超过最大限制数                                         |Number of properties over limitation              |
| 100051         | 规则引擎无订阅Topic权限                                         |Rule engine subscribe topic permission denied              |
| 100052         | 账号下产品数量超过限制                                         |Product under account over limitation              |
| 100053         | API访问过于频繁                                         |Access API too frequent              |
| 100054         | 产品已发布                                         |Product published              |
| 100055         | 产品下的Topic数超过限制                                         |Topic under product over limitation             |
| 100056         | 账户下的规则数量超过限制                                         |Rule under account over limitation             |
| 100057         | 规则下的Action数量超过限制                                         |Action under rule over limitation             |
| 100058         | 物模型属性未定义                                         |Thing model property not define             |
| 100059         | 完成实名认证后可创建更多资源                                         |Create more resources after verifying identity             |
