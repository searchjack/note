#初始启动 MySQL
	/etc/rc.d/init.d/mysqld start

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
在[mysqld]的段中加上一句：skip-grant-tables 
例如： 
[mysqld] 
datadir=/var/lib/mysql 
socket=/var/lib/mysql/mysql.sock 
skip-grant-tables 
保存并且退出vi。 

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
mysql> UPDATE user SET Password = password ( 'new_pass' ) WHERE User = 'root' ; 
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
	
	
	



