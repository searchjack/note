>	this is sth about me how to use Ubuntu.

#	flash player (adbobe flash player)

>	install flash player on ubuntu

<li> get ```install_flash_player_11_linux.x86_64.tar.gz```
  from ```http://get.adobe.com/flashplayer/otherversions/```
> 

# 安装ibus 五笔输入法
```sudo apt-get install ibus-table-wubi```

# jdk 1.6
download:  ```http://www.oracle.com/technetwork/java/javase/archive-139210.html```
迅雷下载: ```http://download.oracle.com/otn-pub/java/jdk/6u38-b05/jdk-6u38-linux-x64.bin```

更改文件权限为可执行 ```chmod u+x jdk-6u14-linux-i586.bin``` or
```chmod 701 jdk-6u14-linux-i586.bin```

- ```sudo ./jdk-6u14-linux-i586.bin```

- 添加环境变量

```sudo gedit /etc/profile```
在profile文件最后添加

	#set java environment
	
	JAVA_HOME=/home/username/develop/jdk1.6.0_14
	export JRE_HOME=/home/username/develop/jdk1.6.0_14/jre
	
	export CLASSPATH=$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
	export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH 

<li> 测试  java -version


