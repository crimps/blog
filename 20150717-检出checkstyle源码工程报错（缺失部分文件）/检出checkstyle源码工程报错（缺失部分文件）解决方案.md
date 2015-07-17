##检出checkstyle源码工程报错（缺失部分文件）解决方案
最近公司小组内部要进行codereview的工作，但是目前的状况是提交的代码的格式都是乱的更别说是逻辑了。虽说开发工具也配置了代码的模板，但是还是有无视一大堆的waring而提交代码的行为，最后只能在代码提交之后再做一次检查。
  
对于Java代码当然用checkstyle了，在使用过程中发现checkstyle相当的好用，于是心血来潮想学习一下源码，就从github上导出了源码，问题就出现了。
  
具体问题就是import部分提示找不到对应的java文件，例如

说是在grammars文件夹下本来应该有GeneratedJavaTokenTypes这个类的，但是实际情况却没有，第一反应是从github导出来的时候文件缺失了，赶紧上github看一下checkstyle项目文件列表，grammars下只有可怜的两个文件。实在想不明白这是怎么回事，还望知情的大神告知一下。
  
没有java文件就自己找加上去不就行了，于是就一个一个的找文件了。具体的缺失文件如下([缺失文件下载地址](https://github.com/damon-cwz/personalBlog/tree/master/20150717-%E6%A3%80%E5%87%BAcheckstyle%E6%BA%90%E7%A0%81%E5%B7%A5%E7%A8%8B%E6%8A%A5%E9%94%99%EF%BC%88%E7%BC%BA%E5%A4%B1%E9%83%A8%E5%88%86%E6%96%87%E4%BB%B6%EF%BC%89/java))：
  
* com.puppycrawl.tools.checkstyle.grammars.GeneratedJavaLexer.java
* com.puppycrawl.tools.checkstyle.grammars.GeneratedJavaRecognizer.java
* com.puppycrawl.tools.checkstyle.grammars.GeneratedJavaTokenTypes.java
* com.puppycrawl.tools.checkstyle.grammars.javadoc.JavadocLexer.java
* com.puppycrawl.tools.checkstyle.grammars.javadoc.JavadocParser
* com.puppycrawl.tools.checkstyle.grammars.javadoc.JavaDocParserListener
* com.puppycrawl.tools.checkstyle.grammars.javadoc.JavaDocParserVisitor
  
(ps:发现一个查找java文件不错的网站[GrepCode](http://grepcode.com/))



