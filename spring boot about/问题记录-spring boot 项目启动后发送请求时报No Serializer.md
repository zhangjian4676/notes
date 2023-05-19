# 问题记录-spring boot 项目启动后发送请求时报No serializer found for class com.lin.pojo.TestVo.TextVo and no properties discovered to create BeanSerializer (to avoid exception, disable SerializationFeature.FAIL_ON_EMPTY_BEANS) (through reference chain: com.lin.common.api.Request["data"])

问题原因：按意思是序列化出了问题。

解决方案：在配置文件application加入如下代码

```
//yml配置文件
spring:
  jackson:
    serialization:
      FAIL_ON_EMPTY_BEANS: false
```

```
//properties配置文件
spring.jackson.serialization.FAIL_ON_EMPTY_BEANS: false
```

