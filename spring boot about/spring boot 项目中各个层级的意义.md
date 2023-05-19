# spring boot 中各个层级的作用

![image-20230512095117156](D:\fantai\JAVA\notes\spring boot about\spring boot 项目中各个层级的意义\image-20230512095117156.png)

**1、用户接口层（Controller层）**

用户接口层主要负责向用户显示信息和解释用户指令，这一层主要做请求的下发和参数校验。

**2、应用层（BIZ层）**

应用层是主要面向用例和流程相关的操作

- 编排多个服务完成业务操作；
- 调用其他微服务的应用服务，完成微服务之间服务的组合和编排
- DTO之间的转换

应用服务是在应用层的，它负责服务的组合、编排和转发，负责处理业务用例的执行顺序以及结果的拼装，以粗粒度的服务通过 API 网关向前端发布。还有，应用服务还可以进行安全认证、权限校验、事务控制、发送或订阅领域事件等。

**3. 业务服务层（service层）**

**业务服务层**的作用是实现核心业务逻辑，通过各种校验手段保证业务的正确性。它用来表达业务概念，业务状态和业务规则,事务只能加在这一层。

```Java
层级要求                       ->  mapper
controller -> biz -> service  -> manager -> mapper

controller层：对外接口，负责请求的转发和参数的校验
biz：业务封装，dto的转化，将do->resp传输到controller,接收controller 的req->do
service：原子性的service能力
manager：mybatis-plus的增强方法
mapper: mybatis crud方法


```