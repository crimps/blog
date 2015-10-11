最近布署在服务器上的一个tomcat服务一天左右就服务中断必须重启，服务中断的原因一时半会也不好找所以一个临时性的解决方案就此产生：每天定时重新启动tomcat服务。

定时重启tomcat可以分有两个部分：1、tomcat重启执本；2、linux定时执行重启脚本

##步骤1：tomcat重启脚本
tomcat重启脚本思路：

1. 使用losf -i:port 指令，根据tomcat占用端口来获取对应的pid
2. 判断tomcat对应的pid是否存在
	- 若pid存在，则使用kill -9 pid指令，杀死tomcat进程，然后执行tomcat启动脚本
	- 若pid不存在，说明tomcat服务并没有启动，则直接执行tomcat启动脚本
	
	
具体代码如下：

```
pid = `lost -i:7788 | awk '{print $2}' | grep -v PID`
echo =======$pid=======
if { -n "$pid" }
then
{
	echo ==================running now====================
	sleep 2
	if { -n "$pid" }
	then
	{
		echo ================kill start===================
		kill -9 $pid
		echo ================kill end=====================
		sleep 2
		echo ================restart now==================
		cd /opt/apache-tomcat-6.0.44
		./bin/startup.sh
	}
	fi
}
else
echo ==================start now=================
cd /opt/apache-tomcat-6.0.44
./bin/startup.sh
echo ==================start end=================
fi
```
##步骤2：linux定时执行脚本
linux定时执行任务则是使用crontab实现  
linux中，周期执行的任务一般由cron这个守护进程来处理，cron读取一个或多个配置文件，这些配置文件中包含了命令行及其调用时间。cron的配置文件称为“crontab”，是“cron table”的简写。

1. 编写cron配置文件:restart.corn，设置每天tomcat重启的时间点
2. 执行 crontab restart.corn,添加定时任务

cron配置文件代码具体如下：

```
0 1 * * * /home/user/restart.sh
//定义在每天的凌晨一点执行任务
```
（ps:在关corntab更详细的内容可自行 man corntab，此处就不多作详细说明）

##最后的最后
不得不吐槽一下，虽说这是一个临时的解决方案但是结果可想而知随着问题的解决，对于tomcat服务中断问题的排查可能就不会再有人提起了。这个问题很有可能就这样一直被人遗忘，直到不知什么时候再次出现坑了不知哪个倒霉的人。

不禁想起当年在杨博士的软件实施的课上听到的那一些软件奇葩的解决方案，当时只是当作笑话来听，现在一想还是自己太年轻了。


















