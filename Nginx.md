启动nginx时 提示:error while loading shared libraries: libpcre.so.1: cannot open shared object file: No such file or directory 
解决方法: 
	32位系统 [root@sever lib]# ln -s /usr/local/lib/libpcre.so.1 /lib 
	64位系统 [root@sever lib]# ln -s /usr/local/lib/libpcre.so.1 /lib64
 