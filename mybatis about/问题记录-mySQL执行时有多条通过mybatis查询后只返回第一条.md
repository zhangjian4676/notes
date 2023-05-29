# 问题记录-mysql执行时有多条记录，通过mybatis查询后只返回了第一条

问题描述：

在controller中传入了一个类型为Long[] scriptId，需要通过scriptId返回数据库中的名称。

在service传递给mapper时将scriptId转换为字符串传递。

```
@Override
public List<String> getList(Long[] scriptId){
    String scriptIds = StringUtils.join(scriptId,",");
    return planScriptManager.getList(scriptIds);
}
```

在mapper.xml文件中接收了字符串。导致查询后的数据只返回了第一条。

```
<select id="getList" resultType="String">
    select
    name
    from t_plan_script
    where
    deleted = 0
    and id in (#{ids})
</select>
```

解决方案：

在service传递给mapper时无需转换为字符串。

```
@Override
public List<String> getList(Long[] scriptId){
    return planScriptManager.getList(scriptId);
}
```

在mapper.xml文件接收时以array接收。通过mybatis中的foreach转换，拼接为以”,“分割的字符串拼接。

```
<select id="getList" resultType="String">
    select
    name
    from t_plan_script
    where
    deleted = 0
    and id in
    <foreach item="item" index="index" collection="array" open="(" separator="," close=")">
        #{item}
    </foreach>
</select>
```

同理，在通过List也可以传递到mabtis，也是通过foreach进行转换。