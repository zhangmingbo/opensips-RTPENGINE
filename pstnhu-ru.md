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

