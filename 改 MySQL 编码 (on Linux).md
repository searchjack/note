#有时候因为编码需要修改mysql的编码，linux大家就可以参考下面的方法

> form :  http://www.jb51.net/article/30104.htm

 
默认登录mysql之后可以通过SHOW VARIABLES语句查看系统变量及其值。

	mysql> show variables like '%character%';

说明：以下是在CentOS-6.2下的设置  （不同的版本可能有些差异，比如文件的位置。但设置的内容应该是一样的)
<li> 1. 找到mysql的配置文件，拷贝到etc目录下，第一步很重要
　　把/usr/share/doc/mysql-server-5.1.52/my-large.cnf 复制到 /etc/my.cnf
　　即用命令：cp /usr/share/doc/mysql-server-5.1.52/my-large.cnf  /etc/my.cnf
<li> 2. 打开my.cnf修改编码
　　在[client]下增加

	default-character-set=utf8
在[mysqld]下增加

	default-character-set=utf8
同时加上

	init_connect='SET NAMES utf8' 
(设定连接mysql数据库时使用utf8编码，以让mysql数据库为utf8运行)

 
<li> 3.重新启动mysql

	service mysqld restart
再次输入

	show variables like '%character%';

 
<li> 即使做了以上修改如果直接数据库再创建表，然后存入中文，取出来的会是问号。解决的办法是：创建数据库的时候指明默认字符集为utf8，如：

	create database test default character set utf8;