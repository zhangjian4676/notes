# 问题记录-windows命令行进入redis

1、win+R进入命令行界面。

2、切换到redis安装目录。

```
cd C:\Program Files\Redis
```

3、进入redis命令。

```
redis-cli.exe -h 8.218.116.162 -p 6379
```

4、输入redis密码。

```
auth 123321123
```

5、查看所有的key。

```
keys *
```

6、切换redis数据库。

```
select 1
```

![image-20230520151851481](D:\fantai\JAVA\notes\redis about\问题记录-进入redis\image-20230520151851481.png)