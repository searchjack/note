# Tomcat 启动提示某 web app 不存在
> from:  http://hi.baidu.com/yeshendong/item/dba325ba99e1c6f063388ed3

<li> 问题:  在 webapp/ , conf/server.xml 中都不存在该项目时， 提示项目不存在

	Tomcat 6.0\webapps\manager does not exist or is not a readable directory
>
严重: Error starting static Resources 
java.lang.IllegalArgumentException: Document base D:\Program Files\Apache Software Foundation\Tomcat 6.0\webapps\host-manager does not exist or is not a readable directory 

或者:
>
严重: Error starting static Resources 
java.lang.IllegalArgumentException: Document base D:\Program Files\Apache Software Foundation\Tomcat 6.0\webapps\manager does not exist or is not a readable directory 


<li> 解决
我们就把

	conf\Catalina\localhost

相应配置文件删掉、把conf下的server.xml及context.xml中的相关配置删掉

OK ! Done.




#	Tomcat 启动是卡在这里：Initializing Spring root WebApplicationContext
> from : http://blog.csdn.net/ksqqxq/article/details/7520712


<li>
>	springtomcat数据库服务器数据库applicationarchive
	一天，突然接到电话，说系统不能发送短信了。检查了web 应用，发现没什么问题，以为是程序中的某个线程挂起了，那直接重启下web 服务器吧。这时，问题来了，tomcat根本不能启动。总是卡在Initializing Spring root WebApplicationContext处。卡在此处，说明spring启动加载什么东西卡住了。看看localhost-04-26.log，显示Deploying web application archive employee- reward.war。这个时候怀疑oracle数据库是否挂了，用tnsping也能ping地通，但用PL\SQL远程登则不行。这很可能说明Spring在加载数据库信息的时候，总是得不到数据库的回应，所以就卡在哪里了。重启数据库服务器，问题解决

<li>
> 解决： 启动数据库
