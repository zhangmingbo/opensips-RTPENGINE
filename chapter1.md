## opensipsctl

1. opensipsctl domain show   命令输出 500 command 'domain\_dump' not available
   解决：在cfg配置文件里加载domain.so                                                                                                                                             loadmodule "domain.so"
   \# ----- domain params -----
   modparam\("domain", "db\_url",
   "mysql://opensips:opensipsrw@localhost/opensips"\)
2. opensips 运行一晚之后，连接数据库的连接数达到600，在连接数据库的module下设置了最大连接数不能解决该问题\(db\_max\_async\_connection=100\)，后来在所有使用mysql 模块下加参数 db\_max\_async\_connections=20；
3. syntax error, unexpected '\[' in /var/www/html/opensips-cp/web/tools/system/drouting/template/rules.main.php on line 155
   在代码里面删除errorInfo\(\)\[2\]里面的'\[2\]'
4. reload server时提示could not connect to host \(json:47.97.213.3:8888/json\)

cfg文件里mi\_json配置错误，正确配置如下：

\#\#\#\# HTTPD module

loadmodule "httpd.so"

modparam\("httpd", "ip", "192.168.1.59"\)

modparam\("httpd", "port", 8888\)

modparam\("httpd", "buf\_size", 524288\)

modparam\("httpd", "post\_buf\_size", 4096\)

loadmodule "json.so"

loadmodule "mi\_http.so"

loadmodule "mi\_json.so"

modparam\("mi\_json", "mi\_json\_root", "json"\)

另外boxes.global.inc.php配置为：

$boxes\[$box\_id\]\['mi'\]\['conn'\]="json:47.97.213.3:8888/json";

1.  ERROR:drouting:get\_group\_id: no group for user "18516237700"@"192.168.1.59"   ， ERROR:drouting:do\_routing: failed to get group id
   drouting脚本在cfg文件里未正确配置

正确配置如下：

        \# use DR to route

        if \( !do\_routing\(\) \) {

                send\_reply\("503","No route found"\);

                exit;

                }







