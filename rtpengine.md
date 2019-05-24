[https://github.com/redis/hiredis](https://github.com/redis/hiredis)  在Centos6上安装rtpengine指南

gperf   gperftools

git clean -f -x -d

Can't locate IPC/Cmd.pm in @INC

yum install perl-IPC-Cmd -y

Failed build with ../lib/fix\_frame\_channel\_layout-04.h

Install FFMPEG on Centos

[https://medium.com/@ShinobiSystems/how-to-install-ffmpeg-on-centos-7017f7647caf](https://medium.com/@ShinobiSystems/how-to-install-ffmpeg-on-centos-7017f7647caf)

No package hiredis available 在网站[http://springdale.math.ias.edu/data/puias/unsupported/6/x86\_64/](http://springdale.math.ias.edu/data/puias/unsupported/6/x86_64/)下载安装包，                   手动安装rpm -Uvh  hi~.rpm

No package 'libevent\_pthreads' found

yum remove libevent-devel ,yum install libevent2-devel解决

在kernel-module下执行make报错：No package kernel-devel-2.6.32-696.6.3.el6.x86\_64 available

/lib/modules/2.6.32-696.6.3.el6.x86\_64文件夹里的build文件出错，从网上也找不到该版本的kernal-devel\(yum install kernel-devel-$\(uname -r\)\);

使用yum update，发现新下载了/lib/module/下有新的版本 ，更改kernal-module下Make file  的配置，将uname -r更改为新文件夹的名字 2.6.32-754.14.2.el6.x86\_64

rtpengine启动时提示 CRIT: Fatal error: Missing option --interface

RTPENGINE的配置文件在安装包目录下的etc目录里，样例文件名为 rtpengine.sample.conf

启动时rtpengine  --config-file=FILE

 rtpengine --config-file=rtpengine.conf 提示错误：

 FAILED TO CREATE KERNEL TABLE 0 \(No such file or directory\), KERNEL FORWARDING DISABLED

方法：重新编译iptables-extension 参考（[https://github.com/sipwise/rtpengine\#manual-compilation](https://github.com/sipwise/rtpengine#manual-compilation)）

make: Nothing to be done for \`all'------make之前 make clean解决

make成功之后生成libxt\_RTPENGINE.so文件，并产生文件 /lib64/xtables /usr/include/xtables.h

接着在kernal-module下make ，并执行 xt\_RTPENGINE.ko，出现错误：error inserting 'xt\_RTPENGINE.ko': -1 Unknown symbol in module，重启服务器解决；重启服务器后，uname -r的结果发生变化，可能是这个原因导致的

insmod libxt\_RTPENGINE

