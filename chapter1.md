## opensipsctl

1. opensipsctl domain show   命令输出 500 command 'domain\_dump' not available
   解决：在cfg配置文件里加载domain.so                                                                                                                                             loadmodule "domain.so"
   \# ----- domain params -----
   modparam\("domain", "db\_url",
   "mysql://opensips:opensipsrw@localhost/opensips"\)
2. opensips 运行一晚之后，连接数据库的连接数达到600，在连接数据库的module下设置了最大连接数不能解决该问题\(db\_max\_async\_connection=100\)
3. syntax error, unexpected '\[' in /var/www/html/opensips-cp/web/tools/system/drouting/template/rules.main.php on line 155
   在代码里面删除errorInfo\(\)\[2\]里面的'\[2\]'



