# 问题记录-No suitable driver found for jdbc

问题描述：没有找到合适的jdbc驱动

![1681354958770](D:\fantai\JAVA\notes\java about\问题记录-No suitable driver found for jdbc\1681354958770.jpg)

解决方案：在pom.xml文件中添加jdbc的maven代码

```
<!--mysql驱动-->
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <version>8.0.19</version>
</dependency>
```

![1681356680376](D:\fantai\JAVA\notes\java about\问题记录-No suitable driver found for jdbc\1681356680376.jpg)