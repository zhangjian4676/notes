## 搭建openvpn

服务器配置：阿里云轻量级服务器 CentOS 7.6 

github：https://github.com/Nyr/openvpn-install

1、在连接轻量级服务器之后，在命令面板中根据提示输入：主机地址：8.217.25.215、网络类型：TCP、端口号：1194、网关地址：1.1.1.1、客户端文件名：client12。

2、进入root，下载client12.ovpn文件。

3、在客户端中import file，选择client12.ovpn文件，提示连接成功。

4、关闭防火墙。

5、查看本机IP地址。

6、设置以太网2的IPv4属性，首选DNS填入1.1.1.1，备用DNS输入8.8.8.8。

7、ping www.google.com。

![1680776340500](D:\fantai\JAVA\notes\linux about\搭建openvpn\1680776340500.jpg)

![0e516ae967a6979a62b72e5ecac1b7b](D:\fantai\JAVA\notes\linux about\搭建openvpn\0e516ae967a6979a62b72e5ecac1b7b.png)

![1680776459159](D:\fantai\JAVA\notes\linux about\搭建openvpn\1680776459159.jpg)

![1680776559305](D:\fantai\JAVA\notes\linux about\搭建openvpn\1680776559305.jpg)