## opensipsctl

1.  opensipsctl domain show   命令输出 500 command 'domain\_dump' not available
   解决：在cfg配置文件里加载domain.so                                                                                                                                             loadmodule "domain.so"
   \# ----- domain params -----
   modparam\("domain", "db\_url",
   "mysql://opensips:opensipsrw@localhost/opensips"\)



