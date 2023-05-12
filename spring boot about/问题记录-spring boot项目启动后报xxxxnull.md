#  问题记录-启动项目时报java.nio.channels.UnresolvedAddressException: null情形之一

根本原因：解析yaml文件时，读取变量失败。

解决方案：本地项目在application.yaml文件中读取时，将变量替换为具体常量。

![image-20230426180632885](D:\fantai\JAVA\notes\spring about\问题记录-spring boot项目启动后报xxxxnull\image-20230426180632885.png)

![image-20230426180615535](D:\fantai\JAVA\notes\spring about\问题记录-spring boot项目启动后报xxxxnull\image-20230426180615535.png)