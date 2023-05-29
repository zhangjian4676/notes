# 问题记录-spring boot 项目启动后，自动进入动态调度（指定时间）任务

整体说明：

通过MyEventListener类在项目启动的时候执行planTaskQueueService.addTimeZoneQueue()，业务代码写在这个方法内，获得下次执行时间后，这个方法会把Task丢进DynamicTaskService.add()，到达指定之间后就会执行DynamicTaskService.getRunnable()，这个方法内再次调用task.run()，task.run()再次调用planTaskQueueService.addTimeZoneQueue()。此时相当于循环调用指定时间的任务。

1、创建MyEventListener类。项目启动时，先调用addTimeZoneQueue这个方法，进入指定时间进行执行任务。

```
@Component
public class MyEventListener  {
    @Autowired
    private IPlanTaskQueueService planTaskQueueService;
    // 事件发生时执行
    @PostConstruct
    public void onApplicationEvent(){
        // 处理事件
        System.out.println("应用程序将要启动");
        planTaskQueueService.addTimeZoneQueue();
    }
}
```

2、创建DynamicTaskService类。执行getRunnable()方法时，再次调用Task的run()。相当于进入循环调用。

```
@Component
@Slf4j
@Service("DynamicTaskService")
public class DynamicTaskService {
    /**
     * 以下两个都是线程安全的集合类。
     */
    public Map<String, ScheduledFuture<?>> taskMap = new ConcurrentHashMap<>();
    public List<String> taskList = new CopyOnWriteArrayList<String>();


    private final ThreadPoolTaskScheduler syncScheduler;

    public DynamicTaskService(ThreadPoolTaskScheduler syncScheduler) {
        this.syncScheduler = syncScheduler;
    }

    /**
     * 查看已开启但还未执行的动态任务
     * @return
     */
    public List<String> getTaskList() {
        return taskList;
    }


    /**
     * 添加一个动态任务
     *
     * @param task
     * @return
     */
    public boolean add(Task task) {
        // 此处的逻辑是 ，如果当前已经有这个名字的任务存在，先删除之前的，再添加现在的。（即重复就覆盖）
        if (null != taskMap.get(task.getName())) {
            stop(task.getName());
        }

        //将localdate转换为date
        Date startTime= formate(task.getStart());

        // schedule :调度给定的Runnable ，在指定的执行时间调用它。
        //一旦调度程序关闭或返回的ScheduledFuture被取消，执行将结束。
        //参数：
        //任务 – 触发器触发时执行的 Runnable
        //startTime – 任务所需的执行时间（如果这是过去，则任务将立即执行，即尽快执行）
        ScheduledFuture<?> schedule = syncScheduler.schedule(getRunnable(task), startTime);
        taskMap.put(task.getName(), schedule);
        taskList.add(task.getName());
        return true;
    }


    /**
     * 运行任务
     *
     * @param task
     * @return
     */
    public Runnable getRunnable(Task task) {

        return () -> {
            System.out.println("---动态定时任务运行---");
//            try {
                System.out.println("此时时间==>" + LocalDateTime.now());
                System.out.println("task中设定的时间==>" + task);
                task.run();
//                Thread.sleep(10);
//            } catch (InterruptedException e) {
//                e.printStackTrace();
//            }
            System.out.println("---end--------");
        };
    }

    /**
     * 停止任务
     *
     * @param name
     * @return
     */
    public boolean stop(String name) {
        if (null == taskMap.get(name)) {
            return false;
        }
        ScheduledFuture<?> scheduledFuture = taskMap.get(name);
        scheduledFuture.cancel(true);
        taskMap.remove(name);
        taskList.remove(name);
        return true;
    }

    public Date formate(LocalDateTime localDateTime){
        ZoneId zoneId = ZoneId.systemDefault();
        ZonedDateTime zdt = localDateTime.atZone(zoneId);
        Date date = Date.from(zdt.toInstant());
        return date;
    }
}
```

3、创建PlanTaskQueueServiceImpl类。业务写在这里，dateTime为指定时间，在循环调用时，dataTime为下次任务执行的具体时间。

```
@Service("PlanTaskQueueServiceImpl")
public class PlanTaskQueueServiceImpl implements IPlanTaskQueueService {
	@Override
    public int addTimeZoneQueue(){
        int rowCount = 0;
        // TODO:这边写需要处理的业务。
        LocalDateTime dateTime = LocalDateTime.now();
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        dateTime =  LocalDateTime.of(dateTime.toLocalDate(),LocalTime.of(dateTime.getHour(),dateTime.getMinute()+1,0));
        Task task = new Task("",dateTime);
        DynamicTaskService dynamicTaskService= (DynamicTaskService) ApplicationContextUtil.getBean("DynamicTaskService");
        dynamicTaskService.add(task);
        return rowCount;
    }
}
```

4、创建Task类。实体类，在run()方法中再次调用addTimeZoneQueue()，就进入了循环调用。

```
@Data
public class Task implements ITask {
    public Task(String name,LocalDateTime start){
        this.name=name;
        this.start=start;
    }
    /**
     * 动态任务名曾
     */
    @Override
    public String getName(){
        return name;
    }
    /**
     * 设定动态任务开始时间
     */
    @Override
    public LocalDateTime getStart(){
        return start;
    }
    public String name;
    public LocalDateTime start;
    @Override
    public void run(){
        //加入到队列
        IPlanTaskQueueService planTaskQueueService= (IPlanTaskQueueService) ApplicationContextUtil.getBean("PlanTaskQueueServiceImpl");
        planTaskQueueService.addTimeZoneQueue();
    }
}
```

5、创建ThreadPoolTaskExecutorConfig类。异步线程池ThreadPoolExecutor 配置类。

```
/**
 * 异步线程池ThreadPoolExecutor 配置类
 *
 */
@Configuration
public class ThreadPoolTaskExecutorConfig {
    @Bean
    public ThreadPoolTaskScheduler syncScheduler() {
        ThreadPoolTaskScheduler syncScheduler = new ThreadPoolTaskScheduler();
        syncScheduler.setPoolSize(5);
        // 这里给线程设置名字，主要是为了在项目能够更快速的定位错误。
        syncScheduler.setThreadGroupName("syncTg");
        syncScheduler.setThreadNamePrefix("syncThread-");
        syncScheduler.initialize();
        return syncScheduler;
    }
}
```

5、项目启动后，开始执行。

![image-20230529093849439](D:\fantai\JAVA\notes\spring boot about\问题记录-spring boot 项目启动后自动执行动态调度任务\image-20230529093849439.png)