# 问题记录-解决两个相同对象类型的List取交集、差集

```
// 更新的账号列表数组
List<PlanTaskAccountEntity> accountEntityList = planTaskReq.getAccountEntityList();

// 原有的账号列表数组
List<PlanTaskAccountEntity> planTaskRespList = planTaskService.batchList(planTaskReq);

// 需要新增的账号集合  更新的账号列表数组-原有的账号列表数组
List<PlanTaskAccountEntity> batchAddList = accountEntityList.stream().filter(o -> !planTaskRespList.stream().map(PlanTaskAccountEntity::getAccountId).anyMatch(id -> Objects.equals(o.getAccountId(), id))).collect(Collectors.toList());

// 需要删除的账号集合  原有的账号列表数组-更新的账号列表数组
List<PlanTaskAccountEntity> batchDeleteList = planTaskRespList.stream().filter(o -> !accountEntityList.stream().map(PlanTaskAccountEntity::getAccountId).anyMatch(id -> Objects.equals(o.getAccountId(), id))).collect(Collectors.toList());

// 不变的账号集合
List<PlanTaskAccountEntity> batchDeleteList = planTaskRespList.stream().filter(o -> accountEntityList.stream().map(PlanTaskAccountEntity::getAccountId).anyMatch(id -> Objects.equals(o.getAccountId(), id))).collect(Collectors.toList());
```