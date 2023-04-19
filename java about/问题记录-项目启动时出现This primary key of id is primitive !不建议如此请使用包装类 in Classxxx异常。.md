## 问题记录-项目启动时出现<This primary key of "id" is primitive !不建议如此请使用包装类 in Class:xxx>异常。

问题描述：mybatis-plush框架对数据类型进行判断。

```
Class<?> keyType = tableInfo.getReflector().getGetterType(property);
if (keyType.isPrimitive()) {
	logger.warn(String.format("This primary key of \"%s\" is primitive !不建议如此请使用包装类 in Class: \"%s\"", property, tableInfo.getEntityType().getName()));
}
```

解决方案：将对象中的主键改为非原始类型即可。

```
@Data
public class TbUser {

    @TableId(value = "id", type = IdType.AUTO)
    //private int id;//该行该为下一行写法，重启项目后不再提示"不建议如此请使用包装类"
    private Integer id;

    private String name;
}
```

![1681535851436](D:\fantai\JAVA\notes\java about\问题记录-项目启动时出现This primary key of id is primitive !不建议如此请使用包装类 in Classxxx异常。\1681535851436.jpg)