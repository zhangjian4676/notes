# 问题记录-maven报错：could not find artifact com.xxx-SNAPSHOT 

在pom.xml中添加依赖后，执行compile后，maven报错：

```
Could not find artifact com.linker.hx:hx-account-matrix:pom:1.0-SNAPSHOT in nexus (http://192.1.2.235:8081/nexus/content/groups/public/)
```

问题原因：表示maven在本地仓库找不到这个资源包。或者是资源包下载不完整。

解决方案：

1、在本地的maven仓库中查看资源包是否存在。如果存在，则把存在的资源包先删掉。

2、在IDEA中，在该资源包所在的模块下，执行maven生命周期中的install将资源包安装在本地仓库。

![image-20230519110014141](D:\fantai\JAVA\notes\maven about\问题记录-maven时报错：could not find artiface com.xxx-SNAPSHOT\image-20230519110014141.png)

3、在输出日志中build success后，就可以在本地仓库看到资源包。

**注：在编译整个工程时，要保证仓库中所依赖的资源全部都有。**

4、如果解决通过以上方式解决不了，则可以通过下载资源包，粘贴到对应的maven仓库对应的地址。

5、再次刷新maven解决该问题。