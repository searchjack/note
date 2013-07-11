#Linux启动项管理

- 使用chkconfig命令可以查看在不同启动级别下课自动启动的服务（或是程序），命令格式如下：

>	chkconfig --list

是查看启动状态，也就是是否开机自动启动
>	chkconfig --list servicename

可能输出如下：
openvpn 0：关闭 1：开启 ...... 6：关闭 （0-6 为启动级别 ; 关闭/开启为相应级别下该服务的自动启动选项）

- 改变启动项，命令：

>	chkconfig --level x name on/off

>	chkconfig --level 5 openvpn off

Example :

- 自动启动

1）察看mysql是否在自动启动列表中

	# /sbin/chkconfig –list
2）把MySQL添加到你系统的启动服务组里面去

	# /sbin/chkconfig – add mysql
3）把MySQL从启动服务组里面删除。

	# /sbin/chkconfig – del mysql