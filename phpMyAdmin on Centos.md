#How to install phpmyadmin on centos 6
> from http://www.krizna.com/centos/how-install-phpmyadmin-centos-6/

> Phpmyadmin :

	Phpmyadmin is a free tool used to administrate MySQL . 
	Phpmyadmin supports all major operation with MySQL in GUI mode.

Before configuring Phpmyadmin refer these steps for installing and configuring apache , mysql and php.

1. Apache2 installation and configuration
2. Mysql installation 
3. PHP installation 
4. Testing all together

> PhpMyadmin installation on Centos 6:
Using YUM :

<li> Step 1 » Install/enable EPEL repository . You can find latest repository here ( http://download.fedoraproject.org/pub/epel/6/i386/repoview/epel-release.html )

	[root@localhost ~]# rpm -ivh http://ftp.jaist.ac.jp/pub/Linux/Fedora/epel/6/i386/epel-release-6-8.noarch.rpm

<li> Step 2 » Now update repositories

	[root@localhost ~]# yum update

<li> Step 3 » After updating yum repositories , now you can install phpmyadmin package

	[root@localhost ~]# yum install phpMyAdmin

This command will install phpmyadmin package along with dependencies . please type the package name exactly as phpMyAdmin ( ” M” and “A” –> Uppercase )

<li> Step 4 » Now restart httpd service

	[root@localhost ~]# service httpd restart

Now open the path in your browser ( Eg->  http://192.168.1.1/phpMyAdmin ) . You can see the below screen after entering Mysql root username and password .

install Phpmyadmin centos

<li> Troubleshooting :

> \#2002 – Can’t connect to local MySQL server through socket ‘/var/lib/mysql/mysql.sock’ (2)
The server is not responding (or the local server’s socket is not correctly configured).

( This means your mysql server service is stopped , you must start the service  “service mysql start”)

> You don’t have permission to access /phpMyAdmin/ on this server.

Open 

	/etc/httpd/conf.d/phpMyAdmin.conf
file and find the lines “Deny from All ” and comment those lines and restart httpd service


<li> 修改登陆密码

在phpmyadmin中有个config.inc.php，你可以用记事本打开它，然后在

	[root@west228 /]# find -name config.inc.php
>	/www/wdlinux/wdcp/phpmyadmin/setup/frames/config.inc.php      <b>
	/etc/phpMyAdmin/config.inc.php

	[root@west228 phpMyAdmin]# vim config.inc.php 

>	$cfg['Servers'][$i]['auth_type'] = 'http'; /* 'session' 'config' */
	$cfg['Servers'][$i]['user'] = 'root';
	$cfg['Servers'][$i]['password'] = '*********';   /*  passwd of mysql */
	$cfg['Servers'][$i]['extension'] = 'mysql';          /* DB name */

<li> 若是扔然丰在问题， 可尝试将['host'] 改为 127.0.0.1

	[root@west228 /]# vim /etc/phpMyAdmin/config.inc.php 
>
	$cfg['Servers'][$i]['host']          = '127.0.0.1'; // MySQL hostname or IP address
$cfg['Servers'][$i]['port']          = '';          // MySQL port - leave blank for default port
$cfg['Servers'][$i]['socket']        = '';          // Path to the socket - leave blank for default socket
$cfg['Servers'][$i]['connect_type']  = 'tcp';       // How to connect to MySQL server ('tcp' or 'socket')
$cfg['Servers'][$i]['extension']     = 'mysqli';    // The php MySQL extension to use ('mysql' or 'mysqli')
$cfg['Servers'][$i]['compress']      = FALSE;       // Use compressed protocol for the MySQL connection
                                                    // (requires PHP >= 4.3.0)
$cfg['Servers'][$i]['controluser']   = 'root';          // MySQL control user settings
                                                    // (this user must have read-only
$cfg['Servers'][$i]['controlpass']   = 'chinabt';          // access to the "mysql/user"
                                                    // and "mysql/db" tables).
                                                    // The controluser is also
                                                    // used for all relational
                                                    // features (pmadb)
$cfg['Servers'][$i]['auth_type']     = 'http';      // Authentication method (config, http or cookie based)?
$cfg['Servers'][$i]['user']          = 'root';          // MySQL user
$cfg['Servers'][$i]['password']      = 'chinabt';          // MySQL password (only needed
 