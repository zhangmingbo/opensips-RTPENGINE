1、error while loading shared libraries: libpython2.7.so.1.0: cannot open shared object file: No such file or directory

解决方法如下：

编辑      vi /etc/ld.so.conf 

如果是非root权限帐号登录，使用 sudo vi /etc/ld.so.conf 

添加上python2.7的lib库地址，如我的/usr/local/Python2.7/lib，保存文件

执行 /sbin/ldconfig -v命令，如果是非root权限帐号登录，使用 sudo  /sbin/ldconfig -v。这样 ldd 才能找到这个库，执行python2.7就不会报错了

  


