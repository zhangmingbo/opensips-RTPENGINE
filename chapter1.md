## opensipsctl

1. opensipsctl domain show   命令输出 500 command 'domain\_dump' not available
   解决：在cfg配置文件里加载domain.so                                                                                                                                             loadmodule "domain.so"
   \# ----- domain params -----
   modparam\("domain", "db\_url",
   "mysql://opensips:opensipsrw@localhost/opensips"\)
2. opensips 运行一晚之后，连接数据库的连接数达到600，在连接数据库的module下设置了最大连接数不能解决该问题\(db\__max\__connection\)



