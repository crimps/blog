### 问题
在Mac上启动tomat,报了如下错误
```
Error:Exception thrown by the agent:
java.net.MalformedURLException:Local host name unknown:
java.net.UnknownHostException:XXX:XXX:nodename nor servname provided, or not known
```
### 解决方案
查看/etc/hosts文件内容，存在 127.0.0.1 localhost 这条信息，
但是通过 scutil --get HostName 返回的结果为空，HostName的值并没有被设置。
手动设置默认的host: scutil --set HostName "localhost"。(PS:些处的localhost必须存在于hosts文件当中)