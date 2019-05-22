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

* 


