# 问题记录-spring boot 项目中使用mybatis批量新增

解决方案：

1、请求端传递List数组。

```
[
  {
     "remark": "sed mollit",
     "name": "测试脚本一1",
     "channel": 2,
     "info": "qui1",
     "sourceKey":1
  },
  {
     "remark": "hjgffd2",
     "name": "测试脚本二2",
     "channel": 3,
     "info": "qwer2",
     "sourceKey":2
  },
  {
     "remark": "qww",
     "name": "测试脚本零",
     "channel": 1,
     "info": "22sd",
     "sourceKey":0
  }
]
```

2、在controller层接收List。

```
@PostMapping("/batchAdd")
public BaseResp batchAdd(@Validated(UpdateGroup.class) @RequestBody List<PlanScriptReq> planScriptReqList) {
    return planScriptBiz.batchAdd(planScriptReqList);
}
```

3、在service层创建事务@Transactional(rollbackFor = Exception.class)。如果接收的不是List，则在service层转为List传递到mapper层。

```
@Override
    @Transactional(rollbackFor = Exception.class)
    public BaseResp batchAddPublish(PlanTaskReq planTaskReq){
        String configurationContent = JSONObject.toJSONString(planTaskReq.getPlanTaskPublishReq());
        //请求参数转换为List集合
        List<PlanTaskEntity> planTaskEntityList = planTaskService.convertPlanTaskList(planTaskReq,configurationContent);

		//批量新增后返回的影响行数。在planTaskEntityList的id会返回对应的主键id
        int rowCount =  planTaskService.batchAddTask(planTaskEntityList);
        List<PlanTaskToScriptEntity> planTaskToScriptEntityList =planTaskToScriptService.convertTaskToScriptList(planTaskEntityList,planTaskReq.getScriptId());
        planTaskToScriptService.batchAddTaskToScript(planTaskToScriptEntityList);

        BaseResp pageBaseResp = new BaseResp();
        pageBaseResp.setData(rowCount);
        return pageBaseResp;
    }
```

4、在mapper层的方法中使用@Param("list")传参，在方法上增加@Options(useGeneratedKeys = true, keyProperty = "id")返回新增的主键id。

```
@Options(useGeneratedKeys = true, keyProperty = "id")
int batchAddTask(@Param("list")List<PlanTaskEntity> planTaskEntityList);
```

5、在mybatis的xml的方法中增加useGeneratedKeys="true" keyProperty="id"。

```
<insert id="batchAddTask" useGeneratedKeys="true" keyProperty="id">
    insert into t_plan_task (
    creator_id,create_time,
    account_id,account_nick_name,
    channel,type,
    status,run_status,
    run_pattern,time_setting,
    time_setting_pattern,
    language,configuration_content,
    script_name)
    values
    <foreach collection="list" item="c" separator=",">
        (
        #{c.creatorId},#{c.createTime},
        #{c.accountId},#{c.accountNickName},
        #{c.channel},#{c.type},
        #{c.status},#{c.runStatus},
        #{c.runPattern},#{c.timeSetting},
        #{c.timeSettingPattern},
        #{c.language},#{c.configurationContent},
        #{c.scriptName}
        )
    </foreach>
</insert>
```

6、在配置文件中使用allowMultiQueries=true。可以在sql语句后增加分号，实现多语句批量执行的效果。

```
datasource: #连接池配置
  driver-class-name: com.mysql.cj.jdbc.Driver
  url: jdbc:mysql://127.0.0.1:3306/test?useAffectedRows=true&allowMultiQueries=true&useUnicode=true&characterEncoding=utf-8&useSSL=false&serverTimezone=Asia/Shanghai
  username: root
  password: 123456
```
