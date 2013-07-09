启动nginx时 提示:error while loading shared libraries: libpcre.so.1: cannot open shared object file: No such file or directory 
解决方法: 
	32位系统 [root@sever lib]# ln -s /usr/local/lib/libpcre.so.1 /lib 
	64位系统 [root@sever lib]# ln -s /usr/local/lib/libpcre.so.1 /lib64
 

nginx启动，重启，关闭命令
停止操作
停止操作是通过向nginx进程发送信号（什么是信号请参阅linux文 章）来进行的
步骤1：查询nginx主进程号
	ps -ef | grep nginx
在进程列表里 面找master进程，它的编号就是主进程号了。
步骤2：发送信号
从容停止Nginx：
	kill -QUIT 主进程号
快速停止Nginx：
	kill -TERM 主进程号
强制停止Nginx：
	pkill -9 nginx
