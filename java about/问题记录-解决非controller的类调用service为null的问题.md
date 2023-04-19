## 问题记录-解决非Controller的类调用Service为null的问题

问题描述：在定时程序任务类RobotwanTask中，调用aiStatisticalAnalysisService的insert的方法时，aiStatisticalAnalysisService报空异常。

解决方案：

1、增加ApplicationContextUtil。

```java
@Component
public class ApplicationContextUtil  implements ApplicationContextAware {
    private static ApplicationContext applicationContext;

    public static ApplicationContext getApplicationContext() {
        return applicationContext;
    }

    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        ApplicationContextUtil.applicationContext = applicationContext;

    }

    public static Object getBean(String beanName) {
        return applicationContext.getBean(beanName);
    }
}
```

2、在aiStatisticalAnalysisService类上增加@Service("AiStatisticalAnalysisServiceImpl")注解。

```java
@Service("AiStatisticalAnalysisServiceImpl")
```

3、在任务类RobotwanTask上增加@Component注解。

```java
@Component
```

4、在任务类RobotwanTask里实例化Service对象。

```java
IAiStatisticalAnalysisService aiStatisticalAnalysisService= (IAiStatisticalAnalysisService) ApplicationContextUtil.getBean("AiStatisticalAnalysisServiceImpl");
```

![1681784430342](D:\fantai\JAVA\notes\java about\问题记录-解决非controller的类调用service为null的问题\1681784430342.jpg)