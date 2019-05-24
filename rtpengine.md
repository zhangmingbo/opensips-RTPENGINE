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

