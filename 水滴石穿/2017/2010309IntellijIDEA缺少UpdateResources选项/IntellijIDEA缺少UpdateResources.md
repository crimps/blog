## 问题描述
Intellij IDEA 更改代码热布署时Update选项只有三个："Update classes"、"Redeploy"、"Restart server"。更新页面文件时无法热布署，只能重新启动相当的耗时。  
##解决方案
打开工程的"Run/Debug Configurations"页面，选中"Deployment"Tab页，将"Deploy at the server startup"内的Artifacts更改为以”"exploded"结尾。