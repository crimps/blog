## Mac OS 您需要安装旧 Java SE 6 运行环境才能打开 “XXX”  
又手贱将系统更新到10.12，早上打开app的进候提示"您需要安装旧 Java SE 6 运行环境才能打开 XXX"。因于此app的版本比较旧，当前系统JVM版本为1.8，修改app的info.plist文件，将JVMVersion改成当前版本，并没有什么作用。  
##解决方案
从苹果官网下载javaforosx.dmg并安装，下载地址:https://support.apple.com/kb/DL1572?viewlocale=zh_CN&locale=en_US