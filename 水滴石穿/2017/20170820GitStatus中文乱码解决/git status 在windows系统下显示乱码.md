git status 在windows系统下显示乱码
![中文乱码图](WX20170820-113911@2x.png)
将全局core.quotepath属性置为false即可
```
git config --global core.quotepath false
```
执行后的效果图
![执行后效果图](WX20170820-113953@2x.png)