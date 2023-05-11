# mybatis传参规范

1、在mapper接口类的方法的传参中定义了@Param("planTaskReq")相当于在xxx.xml文件中定义了parameterType="planTaskReq"。xxx.xml的parameterType不需要传入。使用时：planTaskReq.id。Page为mybatis自带的分页类。使用时，在mapper接口类定义好，就能实现分页。

```
@Mapper
public interface PlanTaskMapper extends BaseMapper<PlanTaskEntity> {
    Page<PlanTaskResp> getTaskList(@Param("planTaskReq")PlanTaskReq planTaskReq,@Param("page")Page page);
}
```

```
<select id="getTaskList"  resultType="com.linker.hx.api.model.resp.PlanTaskResp">
    select
    *
    from t_plan_task
    <where>
            <if test="planTaskReq.id != null "> and id = #{planTaskReq.id}</if>
    </where>
</select>
```

2、如果在mapper接口类的方法的传参中只定义了一个@Param("planTaskReq")。则在xxx.xml中可以直接使用对象的属性。

```
@Mapper
public interface PlanTaskMapper extends BaseMapper<PlanTaskEntity> {
    Page<PlanTaskResp> getTaskList(@Param("planTaskReq")PlanTaskReq planTaskReq);
}
```

```
<select id="getTaskList" parameterType="" resultType="com.linker.hx.api.model.resp.PlanTaskResp">
    select
    *
    from t_plan_task
    <where>
    	<if test="planTaskReq.id != null "> and id = #{id}</if>
    </where>
</select>
```