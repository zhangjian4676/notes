# 问题记录-spring boot 项目启动后，定时执行demo

1、在启动类Application中增加@EnableScheduling。

```
@SpringBootApplication(scanBasePackages = {"com.linker.hx", "com.linker.core"})
@EnableFeignClients(basePackages = {"com.linker.hx.api.rpc"})
@EnableScheduling
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

2、新建TaskDemo1类。

```
@Component
public class TaskDemo1 {
    @Scheduled(cron = "1 * * * * ?")
    public void doTask1(){
        // 实际上就是每分钟一次
        Long Id = Thread.currentThread().getId();
        System.out.println("每分钟的第1秒执行一次"+Id);
    }

    @Scheduled(cron = "1/1 * * * * ?")
    public void doTask2(){
        // 分子的1表示从第1秒开始执行，分母表示每隔1秒执行一次。
        // 但分子我们常常写为*，比如每10秒执行一次*/10
        // 如果需要每隔5秒执行一次，就是除以5
        Long Id = Thread.currentThread().getId();
//        try {
//            sleep(3000);
//        }catch (Exception e)
//        {
//            e.printStackTrace();
//        }
        System.out.println("每秒执行一次"+Id);
    }
}
```

![image-20230529102008465](D:\fantai\JAVA\notes\spring boot about\问题记录-spring boot 项目启动后，定时执行demo\image-20230529102008465.png)