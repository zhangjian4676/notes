# 问题记录-java中List转换String字符串的几种方式

**1.使用StringUtils工具类List转String**

```
List<String> list = Arrays.asList("张三", "李四", "王五", "赵六");     
String join = StringUtils.join(list, ",");
```

StringUtils需要添加依赖

```
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.12.0</version>
</dependency>
```

**2.使用guava的Joiner字符串拼接**

```
List<String> list = Arrays.asList("张三", "李四", "王五", "赵六");     
String join2 = Joiner.on(",").join(list);
```

**3.Java8 String.join()**

StringUtils.join() 和 String.join()用途：将数组或集合以某拼接符拼接到一起形成新的字符串。

这里和StringUtils.join()有区别，参数顺序不一样，另外，StringUtils.join(）可以传入Integer或者其他类型的集合或数组，而String.join()尽可以传入实现charSequence接口类型的集合或数组。

如果是字符串类型的集合或数组推荐使用String.join()

```
List<String> list = Arrays.asList("张三", "李四", "王五", "赵六");     
String str = String.join(",", list);
```

**4.Java8 Collctors.joining()**

将分隔符、前缀和后缀作为参数。此方法将列表转换为具有给定分隔符、前缀和后缀的字符串。同样是用于字符串类型的集合。

```
List<String> list = Arrays.asList("1", "2", "3", "4");
String defult = list.stream().collect(Collectors.joining(",", "{", "}"));
```

**5.传统循环并拼接的方式**

```
List<String> list = Arrays.asList("张三", "李四", "王五", "赵六");   
StringBuilder builder = new StringBuilder();
for (int i = 0; i < scriptId.length; i++) {
    builder.append(scriptId[i]);
    builder.append(",");
}
```