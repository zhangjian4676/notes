# 问题记录-git推送时提示，Push failed Remote: Support for password authentication was removed on August 13, 2021. remote

问题原因：2021年8月13日取消了对密码身份验证的支持。

![img](https://img-blog.csdnimg.cn/4c9516bc5012418d88dca0defb9c78a1.png)

解决方案：

1、**打开设置**

在任何页面的右上角，单击您的个人资料照片，然后单击设置。

![img](https://img-blog.csdnimg.cn/7edaabee50284629bd41354ced803cbf.png)

2、**个人访问令牌**

在左侧栏中，选择 Developer settings > Personal access tokens。

![img](https://img-blog.csdnimg.cn/77264af240b64e2db521534c548f7c3b.png)

3、**单击 Generate new token**

4、**配置Token**

起一个Token描述性的名称。

选择Token的到期时间，请选择expiration[下拉菜单](https://so.csdn.net/so/search?q=下拉菜单&spm=1001.2101.3001.7020)，然后单击默认值或使用日历选择器。

选择要授予该Token的作用域或权限。如果要使用的Token支持从命令行[访问GitHub](https://so.csdn.net/so/search?q=访问GitHub&spm=1001.2101.3001.7020)，请选择repo。

点击，Generate token。

![img](https://img-blog.csdnimg.cn/fbc07c2215a74899822d7a6ef2e9004a.png)

5、**获取到Token**

这儿需要注意将Token进行保存下来，或者记录到文本中，刷新页面就没有了，还得重新生成Token！

![img](https://img-blog.csdnimg.cn/743db081238d40b38b44189c9040383f.png)

***注意：****需要像对待密码一样对待你的Token，并对Token保密。在调用API时，使用Token作为环境变量，而不是将Token硬编码到程序中，这是一种极度危险的骚操作，切记！！！**

6、**通过Token登录授权**

![img](https://img-blog.csdnimg.cn/111e5cedc4b94277a80b6b22bbb7f809.png)

7、**提交代码**

通过Token进行登录鉴权后，再次提交代码就可以正常推送了。

![img](https://img-blog.csdnimg.cn/34375bc853fb42288f14382d964672c8.png)