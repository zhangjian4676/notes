## 问题记录-nested exception is org.springframework.boot.web.server.PortInUseException: Port 8080 is already in use

问题描述：8080端口已经被占用。

解决方案：杀死8080占用的进程。

1、win+R，进入命令窗口。

2、netstat -ano，查看所有端口和PID。

3、查找8080对应的PID 19444。

4、taskkill -PID 19444 -f，杀死8080这个进程。

5、再次启动项目。

![1681470401927](D:\fantai\JAVA\notes\java about\问题记录-nested exception is org.springframework.boot.web.server.PortInUseException Port 8080 is already in use\1681470401927.jpg)

