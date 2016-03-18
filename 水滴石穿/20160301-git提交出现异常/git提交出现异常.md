最近push的时候总是提示失败

[fatal: unable to access 'http://github.com/userName/projectName.git/': Recv failure: Connection reset by peer] 

![git提交错误信息](https://raw.githubusercontent.com/damon-cwz/personalBlog/master/%E6%B0%B4%E6%BB%B4%E7%9F%B3%E7%A9%BF/20160301-git%E6%8F%90%E4%BA%A4%E5%87%BA%E7%8E%B0%E5%BC%82%E5%B8%B8/QQ20160301-0%402x.png)

从字面上的意思来看是连接被重置，但是却没有明确的说明被重置的原因.第一反应是git出问题（程序员总是想把问题归结于外部原因的习惯性思维），但是试了其他工程却一点问题都没有看来不是git的问题，只好乖乖找问题了。

在网上找了不少方法，也试了各种各样的方法。最后的最后，看到提示出错的那个链接是http://开头不是https://的。用[git remote set-url origin 新地址]的方法重置远程仓库地址，再次执行push操作，一切功能正常。




