## 解决ClassLoaderUtils中不存在getClazzByArgs方法

问题描述：添加了ClassLoaderUtils的引用之后，仍没有getClazzByArgs方法。

解决方案：在调用ClassLoaderUtils.getClazzByArgs()需要返回Class<?>[]，所以可以自己创建一个相同功能的函数。

```
public static Class<?>[] getClazzByArgs(Object[] args) {
    Class<?>[] parameterTypes = new Class[args.length];
    for (int i = 0; i < args.length; i++) {
        if (args[i] instanceof ArrayList) {
            parameterTypes[i] = List.class;
            continue;
        }
        if (args[i] instanceof LinkedList) {
            parameterTypes[i] = List.class;
            continue;
        }
        if (args[i] instanceof HashMap) {
            parameterTypes[i] = Map.class;
            continue;
        }
        if (args[i] instanceof Long) {
            parameterTypes[i] = long.class;
            continue;
        }
        if (args[i] instanceof Double) {
            parameterTypes[i] = double.class;
            continue;
        }
        if (args[i] instanceof TimeUnit) {
            parameterTypes[i] = TimeUnit.class;
            continue;
        }
        parameterTypes[i] = args[i].getClass();
    }
    return parameterTypes;
}
```

![image-20230420162610547](D:\fantai\JAVA\notes\java about\问题记录-解决ClassLoaderUtils中没有getClazzByArgs\image-20230420162610547.png)