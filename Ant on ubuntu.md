#一 手动安装(推荐)
<li> 1. 下载ant

<li> 2. 解压下载下来的.tar.gz文件： ```tar -zxvf apache-ant-x.x.x-bin.tar.gz```

	在win 下载 apache-ant-*.zip  解压即可
<li> 3. 将解压出来的文件移动到/opt/下：sudo mv apache-ant-1.8.2 /opt/   ```(存放位置看个人习惯)```

<li> 4. 配置环境变量：```sudo gedit /etc/profile```，在原来基础上添加以下蓝体字：

	export ANT_HOME=/opt/apache-ant-1.8.2
	export JAVA_HOME=/usr/lib/jvm/java-6-openjdk
	export PATH=$JAVA_HOME/bin:$PATH:$ANT_HOME/bin
	export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

<li> 5. 验证是否安装成功： ```ant -version```

	Apache Ant(TM) version 1.8.2 compiled on December 20 2010


使用帮助 ant --help





#二 可以使用

	sudo apt-get install ant

