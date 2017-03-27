JDBC连接MySQL数据入库，中文出现乱码，在客户端插入中文数据都正常。JDBC设置编码为UTF-8问题依然存在，就可以确定是由于MySQL服务的默认编码不为UTF-8引起的。
###1、检查默认安装的MySQL的字符集
```
mysql> show variables like '%char%';
+--------------------------+----------------------------
| Variable_name            | Value                                        
+--------------------------+----------------------------
| character_set_client     | utf8                                         
| character_set_connection | utf8                                          
| character_set_database   | utf8                                          
| character_set_filesystem | binary                                        
| character_set_results    | utf8                                          
| character_set_server     | latin1                                        
| character_set_system     | utf8                                         
| character_sets_dir       | /usr/local/mysql-5.6.19-osx10.7-x86/share/charsets/ |
+--------------------------+----------------------------
8 rows in set (0.02 sec)
```
character_set_server是latin1字符集，客户端与服务端的字符集不一致引起了中文乱码。要修改默认字符集，要修改my.cnf，在修改my.cnf之前一定要关闭mysql进程，不然会遇到MySQL的sock不能连接的问题。
###2、关闭MySQL后台进程
在系统偏好设置里面控制MySQL，直接点击"Stop MySQL Server"就行了；
也可以找到MySQL所在的位置，/usr/local/mysql/bin,执行关闭命令。
###3、修改MySQL配置文件/etc/my.cnf
```
sudo cp /usr/local/mysql/support-files/my-medium.cnf /etc/my.cnf
sudo vi /etc/my.cnf
```
[client]部分加入：
default-character-server = utf8
###4、检查结果
```
mysql> show variables like '%char%';
+--------------------------+----------------------
| Variable_name            | Value                                    
+--------------------------+----------------------
| character_set_client     | utf8                                          
| character_set_connection | utf8                                         
| character_set_database   | utf8                                          
| character_set_filesystem | binary                                        
| character_set_results    | utf8                                         
| character_set_server     | utf8                                          
| character_set_system     | utf8                                         
| character_sets_dir       | /usr/local/mysql-5.6.19-osx10.7-x86/share/charsets/ |
+--------------------------+-----------------------
8 rows in set (0.01 sec)
```
所有的编码已经更改为UTF-8字符集。