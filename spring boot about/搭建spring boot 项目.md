## 搭建spring boot 项目

1、新建项目，选择Maven，点Next。

![1681470775021](D:\fantai\JAVA\notes\spring about\搭建spring boot 项目\1681470775021.jpg)

2、输入项目名称，组织，点击Finsh。

![1681470884730](D:\fantai\JAVA\notes\spring about\搭建spring boot 项目\1681470884730-168189597770721.jpg)

3、在pom.xml中添加配置，在Maven。

```
<!--导入springboot 父工程-->
<parent>
    <artifactId>spring-boot-starter-parent</artifactId>
    <groupId>org.springframework.boot</groupId>
    <version>2.5.3</version>
</parent>
<!--导入web项目场景启动器 会自动导入和web开发相关的依赖-->
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

![1681470921295](D:\fantai\JAVA\notes\spring about\搭建spring boot 项目\1681470921295.jpg)

4、添加启动类MainApp.java，启动。

![1681470950318](D:\fantai\JAVA\notes\spring about\搭建spring boot 项目\1681470950318.jpg)