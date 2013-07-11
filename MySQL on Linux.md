<<<<<<< HEAD
#初始启动 MySQL
	/etc/rc.d/init.d/mysqld start
=======
#终止MySQL

    [root@west228 etc]# ps -ef | grep mysql
    root      3955  3693  0 11:15 pts/0    00:00:00 grep mysql
    [root@west228 etc]# kill -quit 3693

#初始启动 MySQL

	#/etc/rc.d/init.d/mysqld start

#初始启动 MySQL
>	/etc/rc.d/init.d/mysqld start

	[root@west228 ~]#   rpm  -qa | grep  mysql
	mysql-libs-5.1.69-1.el6_4.x86_64
	mysql-5.1.69-1.el6_4.x86_64
	mysql-devel-5.1.69-1.el6_4.x86_64
>>>>>>> rm Java.md R.md

#终止MySQL
	[root@west228 etc]# mysql --version
	mysql  Ver 14.14 Distrib 5.1.61, for unknown-linux-gnu (x86_64) using  EditLine wrapper
	[root@west228 etc]# ps -ef | grep mysql
	root      3955  3693  0 11:15 pts/0    00:00:00 grep mysql
	[root@west228 etc]# ^C
	[root@west228 etc]# kill -quit 3955
	-bash: kill: (3955) - 没有那个进程
	[root@west228 etc]# kill -quit 3693
	[root@west228 etc]# mysql --version
	mysql  Ver 14.14 Distrib 5.1.61, for unknown-linux-gnu (x86_64) using  EditLine wrapper
	[root@west228 etc]# mysql -u
	mysql: option '-u' requires an argument
	[root@west228 etc]# mysql -uroot
	ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (111)
	[root@west228 etc]# 


#卸载 MySQL
	[root@west228 ~]# yum -y remove mysql-5.1.69-1.el6_4.x86_64
Loaded plugins: fastestmirror
Setting up Remove Process
Resolving Dependencies
--> Running transaction check
---> Package mysql.x86_64 0:5.1.69-1.el6_4 will be erased
--> Finished Dependency Resolution

Dependencies Resolved

================================================

Package            Arch                Version                      Repository             Size

================================================
Removing:
 mysql              x86_64              5.1.69-1.el6_4               @updates              2.4 M

Transaction Summary

=================================================================================================
Remove        1 Package(s)
......



#MySQL 修改密码 

>	http://www.cnblogs.com/allenblogs/archive/2010/08/12/1798247.html

1．首先确认服务器出于安全的状态，也就是没有人能够任意地连接MySQL数据库。 
因为在重新设置MySQL的root密码的期间，MySQL数据库完全出于没有密码保护的 
状态下，其他的用户也可以任意地登录和修改MySQL的信息。可以采用将MySQL对 
外的端口封闭，并且停止Apache以及所有的用户进程的方法实现服务器的准安全 
状态。最安全的状态是到服务器的Console上面操作，并且拔掉网线。 

2．修改MySQL的登录设置： 

	# vi /etc/my.cnf
在[mysqld]的段中加上一句：

	skip-grant-tables 
例如： 

	[mysqld] 
	datadir=/var/lib/mysql 
	socket=/var/lib/mysql/mysql.sock 
	skip-grant-tables 


3．重新启动 mysqld

	# /etc/init.d/mysqld restart 
Stopping MySQL: [ OK ] 

Starting MySQL: [ OK ] 

4．登录并修改MySQL的root密码 

	# /usr/bin/mysql
	Welcome to the MySQL monitor. Commands end with ; or \g. 
	Your MySQL connection id is 3 to server version: 3.23.56 
	Type 'help;' or '\h' for help. Type '\c' to clear the buffer. 
	mysql> USE mysql ; 

>	mysql> select user,host,password from mysql.user;

	+------+-----------+----------+
	| user | host      | password |
	+------+-----------+----------+
	| root | localhost |          |
	| root | west228   |          |
	| root | 127.0.0.1 |          |
	|      | localhost |          |
	|      | west228   |          |
	+------+-----------+----------+
	5 rows in set (0.00 sec)

>	mysql> USE mysql ;

	Database changed
>	mysql> UPDATE user SET Password = password ( 'new_pass' ) WHERE User = 'root' ; 

	Query OK, 3 rows affected (0.00 sec)
	Rows matched: 3  Changed: 3  Warnings: 0

>	mysql> select user,host,password from mysql.user;

	+------+-----------+-------------------------------------------+
	| user | host      | password                                  |
	+------+-----------+-------------------------------------------+
	| root | localhost | *5143AC362E6D6A0A36D35C009567621C313339AA |
	| root | west228   | *5143AC362E6D6A0A36D35C009567621C313339AA |
	| root | 127.0.0.1 | *5143AC362E6D6A0A36D35C009567621C313339AA |
	|      | localhost |                                           |
	|      | west228   |                                           |
	+------+-----------+-------------------------------------------+
	5 rows in set (0.00 sec)
	
	
#更改MySQL目录
> http://my.oschina.net/pioneeer/blog/31976

MySQL默认的数据文件存储目录为/var/lib/mysql。假如要把目录移到/home/data下需要进行下面几步：

<li> 1、home目录下建立data目录

	cd /home
	mkdir data

<li> 2、把MySQL服务进程停掉： 

	mysqladmin -u root -p shutdown

<li> 3、把/var/lib/mysql整个目录移到/home/data

	mv /var/lib/mysql /home/data/
这样就把MySQL的数据文件移动到了/home/data/mysql下

<li> 4、找到my.cnf配置文件
如果/etc/目录下没有my.cnf配置文件，请到/usr/share/mysql/下找到*.cnf文件，拷贝其中一个到/etc/并改名为my.cnf)中。命令如下：

	[root@test1 mysql]# cp /usr/share/mysql/my-medium.cnf /etc/my.cnf

<li> 5、编辑MySQL的配置文件/etc/my.cnf
为保证MySQL能够正常工作，需要指明mysql.sock文件的产生位置。 修改socket=/var/lib/mysql/mysql.sock一行中等号右边的值为：/home/mysql/mysql.sock 。操作如下：
vi my.cnf (用vi工具编辑my.cnf文件，找到下列数据修改之)

	#The MySQL server
	[mysqld]
	port = 3306
	#socket = /var/lib/mysql/mysql.sock（原内容，为了更稳妥用“#”注释此行）
	socket = /home/data/mysql/mysql.sock （加上此行）

<li> 6、修改MySQL启动脚本/etc/rc.d/init.d/mysql
最后，需要修改MySQL启动脚本/etc/rc.d/init.d/mysql，把其中datadir=/var/lib/mysql一行中，等号右边的路径改成你现在的实际存放路径：home/data/mysql。
[root@test1 etc]# vi /etc/rc.d/init.d/mysql

	#datadir=/var/lib/mysql （注释此行）
	datadir=/home/data/mysql （加上此行）

<li>7、重新启动MySQL服务

	/etc/rc.d/init.d/mysql start
或用reboot命令重启Linux
如果工作正常移动就成功了，否则对照前面的7步再检查一下。	



<li>chkconfig 功能说明：检查，设置系统的各种服务。
语　法：

删除启动项:

	chkconfig [--add][--del][--list][系统服务] 
或是否自启动

	chkconfig [--level <等级代号>][系统服务][on/off/reset]
