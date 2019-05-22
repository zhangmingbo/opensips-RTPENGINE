The drouting module is intended for prefix-based routing to a set of gateways

以下是dynamic routing的特性

Routing rule selection（路由规则选择）

* 基于前缀
* 基于主叫/组
* 基于时间
* 基于优先级

Call processing路由处理

* 去前缀或加前缀
* 默认路由规则
* 呼入呼出处理
* 脚本路由触发
* 多网关处理

* 失败重路由

* 权重负载

* 运营商概念

路由数据（目的，规则，运营商）存储在mysql数据库里，在opensips启动时缓存到本地，路由前缀被重新组织为搜索树，查询时间由前缀的长度而非规则的数量；数据可通过'dr\_reload' MI 命令重新加载。

路由实体（Routing entities）

* 网关\(gateway\)是终端SIP实体，路由的目的地；网关的定义存储在dr\_gateways表中，gateway ID有唯一性；
* 运营商（carrier）概念用于将网关分组，便于控制网关们在路由规则的使用，如网关的路由顺序；数据存储于dr\_carriers表；

路由规则是控制基于前缀路由的实际规则。使用不同的标准（prefix，time，priority等），决定呼叫将会发送到哪些网关上。

规则定义的默认表名称是dr\_rules，每一条规则可能是一条或多条路由的一部分；规则组用于将规则分组，例如：你可以有一组规则用来实现best-effor质量路由，其它组用来实现高质量路由。（使用不同的网关来提供不同的质量）

![](/assets/import2.png)

## 路由规则详解

![](/assets/import3.png)

首先，查找路由组（set/group），该组可能提供脚本级别的路由（do_routing\(\)）,如果没有，则通过查找dr\_groups表，找到基于From消息头的组_

组确定之后，开始匹配被叫号码前缀，选择最长的前缀匹配成功的规则；如果没有匹配到，则选择默认路由；

下一步匹配时间，如时间表达式为空，则默认没有规则；

当时间规则匹配后，接下来根据优先级排序，数值大的规则，优先级更高；

被选择的路由规则包含一组网关或者运营商（gateways or carriers），该模块会将电弧发送至其中一个网关；网关列表的排序方式有2种：

给与的顺序；基于权重重新排序；

CarrierA – GW1=25, GW2=75 \(using weights\)

CarrierB – GW3,GW4 \(no weights\)

Rule for prefix 4021 \(no W flag\) : \#CarrierA,\#CarrierB, GW5

Results:

GW1, GW2, GW3, GW4, GW5

GW2, GW1, GW3, GW4, GW5

CarrierA may have a different order due to the weightbased

reordering，运营商A可能会有不同的顺序，因为有权重因子（权重大的并不代表只选择大的）

If a

gateway fails \(no answer or server error reply\), you can do serial forking via the failure

route and try the next available gateway from the selected rule.

