# 1、信任认证网关：一般通过IP地址来授信

## 认证方法一

可通过静态配置的方式，将IP地址写入路由脚本文件里：

if \( \($si=="10.10.10.5" && $sp==5060 && $proto=="UDP"\) \|\|

\($si=="10.10.10.9" && $sp==5060 && $proto=="UDP"\) \) {

\# trusted GW, skip digest authentication

}

## 认证方法二

加载Permissions 模块：模块允许管理多个IP地址或地址段，地址可按照不同的目的进行分组，如网关组，sipserver组等

IP地址存储于address表，opensips启动时被加载到缓存里，可通过‘address\_reload’ MI命令实时更新。

permissions模块提供灵活的函数，check\_address  \(group,IP, port ,proto\) 多维度，而不仅仅只是验证网络IP地址；

# 2、被叫号码处理

呼入时被叫号码为PSTN号码，该号码应该要被映射为本地小号或路由点；

## 方法一 脚本文件编辑路由

if \( check\_source\_address\("1"\) \) {

\# trusted GW, normalize to E.164

if \( $rU=~"^00" \) { \# international 00 format

strip\(2\);

} else if \( $rU=~"^+" \) { \# international + format

strip\(1\);

}

## 方法二  dialplan 模块处理

loadmodule "dialplan.so"

modparam\("dialplan","db\_url", "mysql://user:pwd@localhost/opensips"\)

{ ..

if \( check\_source\_address\("1"\) \) {

\# trusted GW, normalize to E.164

if \( !dp\_translate\("10","$rU/$rU"\) \) {

send

![](/assets/import.png)

号码确定后，接下来查询本地服务号码的归属。

考虑到PSTN号码其实是实际服务或者用户的化名，我们可以用Aliasing System

loadmodule "alias\_db.so"

modparam\("alias\_db","db\_url", "mysql://user:pwd@localhost/opensips"\)\# use the "dids" aliases table and do not

\# use the domain part when looking up for alias

if \( alias\_db\_lookup\("dids","d"\) \) {

send\_reply\("404","DID not found"\);

exit;

}

alias\_db module实时查询数据库，因此如果号码量特别大的话，考虑到效率问题，应该是用缓存接口（cached interface）

drouting模块也可以做DID到内部号码的映射，支持缓存方式。

