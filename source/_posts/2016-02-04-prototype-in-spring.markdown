---
layout: post
title: "Spring中原型prototype的准确使用"
date: 2016-02-04 16:55:01 +0800
comments: true
categories: spring
---

## 实际问题


项目中，报表导出涉及到了在同一个类的两个不同方法中，都有相同的查询数据库的操作，一个方法是用于获取内容，一个是用于获取条数的，大概类似于这样：
``` java
@Service
public class MyReportExporter extends AbstractReportExporter{
	@Override
    protected DataResp getData(Param param) {
        List records = myService.queryList(param);//查询db
        return wrapResp(records);
    }
    
	@Override
    protected int getCount(Param param) {
        return myService.queryList(param).size();//查询db
    }
}
```
由于是继承的父类统一处理，因此没办法单独优化这个步骤。在父类的统一处理过程中，会多次调用getCount方法，这样每处理一次，就需要多次查询数据库。

这是会想到，可以用私有全局变量将查询结果存起来。

## 使用原型

在Spring中，@Service默认都是单例的。用了私有全局变量，若不想影响下次请求，就需要用到原型模式，即@Scope("prototype")

所谓单例，就是Spring的IOC机制只创建该类的一个实例，每次请求，都会用这同一个实例进行处理，因此若存在全局变量，本次请求的值肯定会影响下一次请求时该变量的值。
原型模式，指的是每次调用时，会重新创建该类的一个实例，比较类似于我们自己自己new的对象实例。

通过查看@Scope我们可以看到，默认的模式：singleton
``` java
public @interface Scope {
String value() default ConfigurableBeanFactory.SCOPE_SINGLETON;
...
}
```
通过如下方式，可以将该类设置为原型模式
```java
@Service
@Scope("prototype")
public class MyReportExporterextends AbstractReportExporter{
	...
}
```
##prototype陷阱
在进行以上改动后，运行发现并没有生效，依然是一个实例。这说明只加一个@Scope注解还不够。

在调用改service的controller层，是这样注入的：
``` java
    @Autowired
    private MyReportExporter myReportExporter;
```
而controller同样是默认单例的，因此只实例化了一个controller对象，在其中依赖注入的MyReportExporter对象也就只会实例化一次。

在不想改变controller单例模式的情况下，可以如下修改：
放弃使用@Autowired方式，改用getBean方式：
```java
private static ApplicationContext applicationContext;
MyReportExporter myReportExporter = applicationContext.getBean(MyReportExporter.class);
```

可以自己写个Spring工厂类，如下：
```java
import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;

import com.quhuhu.cesar.common.utils.LogUtils;

public class SpringBeanFactory implements ApplicationContextAware {

    private static ApplicationContext applicationContext;

    @Override
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
        this.applicationContext = applicationContext;
    }

    /**
     * 获取某个Bean的对象
     */
    public static <T> T getBean(Class<T> clazz) {
        try {
            return applicationContext.getBean(clazz);
        } catch (Exception e) {
            LogUtils.errorMail("Spring getBean:" + clazz, e);
        }
        return null;
    }
}
```
然后，通过如下方式调用：
```java
SpringBeanFactory.getBean(MyReportExporter.class).doSth()
```
修改后，运行OK，达到自己想要的结果。

## 小结

Spring中依赖注入的默认对象为单例形式，@Scope(“prototype”)注解可以将其改变为原型模式。

改变底层（如service层）的对象为原型时，同时改变上层调用层（如controller层）的调用方式，原型模式才会生效。