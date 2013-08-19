> this is sth about me how to use Ubuntu.

# flash player (adbobe flash player)

> install flash player on ubuntu

- via:  [linux公社](http://www.linuxidc.com/Linux/2012-11/73629p2.htm)

<li> get ```install_flash_player_11_linux.x86_64.tar.gz```
  from ```http://get.adobe.com/flashplayer/otherversions/```
>
	
	sudo cp libflashplayer.so /usr/lib/mozilla/plugins/
	cp -r ./usr/* /usr/



# ibus 五笔输入法
- via: [blogjava](http://www.blogjava.net/leisure/archive/2011/11/06/358567.html)
启动 ibus 输入法 ```Keyboard Input Methods```

```sudo apt-get install ibus-table-wubi```

>
开机启动，要在```Language Support```
里选择```Keyboard input method system```为```ibus```就可以了。




# jdk 1.6
- download:  [java](http://www.oracle.com/technetwork/java/javase/archive-139210.html)
迅雷下载: [jdk-6u38-linux-x64.bin](http://download.oracle.com/otn-pub/java/jdk/6u38-b05/jdk-6u38-linux-x64.bin)

- 更改文件权限为可执行 ```chmod u+x jdk-6u45-linux-x64.bin``` or
```chmod 701 jdk-6u45-linux-x64.bin```


- ```sudo ./jdk-6u45-linux-x64.bin```  // 将 .bin 文件放到安装目标目录


- 添加环境变量

```sudo gedit /etc/profile```  在profile文件最后添加

	#set java environment
	
	JAVA_HOME=/home/searchjack/develop/jdk1.6.0_45
	export JRE_HOME=/home/searchjack/develop/jdk1.6.0_45/jre
	
	export CLASSPATH=$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
	export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH


- 重启后，测试  java -version




＃ 设置中文字体

来自 ubuntu 的字体下载提示, [font](http://wiki.ubuntu.org.cn/%E5%AD%97%E4%BD%93)

```可用字体```
>
sudo apt-get install ttf-wqy-microhei  #文泉驿-微米黑
sudo apt-get install ttf-wqy-zenhei  #文泉驿-正黑
sudo apt-get install xfonts-wqy #文泉驿-点阵宋体


- 手动修改字体：
via: [install fonts](http://single9.net/2012/11/ubuntu-12-04-%E4%BF%AE%E6%94%B9%E8%8B%B1%E6%96%87%E7%95%8C%E9%9D%A2%E9%A0%90%E8%A8%AD%E4%B8%AD%E6%96%87%E5%AD%97%E9%AB%94%E3%80%82/)

> sudo gedit /etc/fonts/conf.d/65-nonlatin.conf
	
找到 ```sans-serif``` 在<prefer>後加上新的一行

```<family>WenQuanYi Micro Hei</family>```

再找到 ```monospace``` 一樣在<prefer>後加上新的一行

```<family>WenQuanYi Micro Hei Mono</family>```

最後執行 ```$ sudo fc-cache -v```
清掉字体缓存，到這邊已經大功告成，你可以嘗試把這個瀏覽器關掉，然後在一次打開，你會發現中文果然變得養眼多了。





