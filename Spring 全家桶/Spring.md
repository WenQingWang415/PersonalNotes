## Spring

#### IOC：控制反转

> 控制反转：是一个思想，概念，理论
>
> 概述：把对象的创建，赋值，管理工作交给代码外的容器实现，对象的创建是其他外部资源完成的
>
> 控制：创建对象，属性的赋值，对象之间的管理关系
>
> 反转：把以前的开发人员管理的对象，赋值全部交给容器实现
>
> 容器：服务器的软件，一个框架
>
> 为什么使用ICO：实现解耦

#### IOC的技术实现

> DI是IOC的技术实现
>
> DI：依赖注入，只需要在程序中提供名称就可以，至于对象如何在容器中创建，赋值，查找都是由容器内部实现
>
> Spring是使用的DI实现了IOC的功能，Spring底层创建对象，依然是使用的反射机制



#### Spring创建对象的整个过程

> 1.创建接口以及实现
>
> ```java
> //创建接口
> public interface Someservice {
>     void  sode();
> }
> ```
>
>   ```java 
> //实现接口
> public class SomeserviceIMp  implements   Someservice{
>     @Override
>     public void sode() {
>         System.out.println("打印");
>     }
> }
>   ```
>
> 2.创建配置文件
>
> ```java
> <?xml version="1.0" encoding="UTF-8"?>
> <beans xmlns="http://www.springframework.org/schema/beans"
>        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>        xsi:schemaLocation="http://www.springframework.org/schema/beans
>        http://www.springframework.org/schema/beans/spring-beans.xsd">
>     <!--告诉spring创建对象，其实申明bean标签-->
>     <!--ID 是唯一的值，class 只能是类不能是接口，因为需要反射-->
>     <bean id="somecervice" class="com.spring.wenqingwang.service.imp.SomeserviceIMp"></bean>
>      <!--spring可以创建非自定义对象-->
>     <bean id="mydate" class="java.util.Date"/>
> </beans>
> ```
>
> 3.spring容器创建对象
>
> ```java 
>        //使用spring容器创建对象
>        /**
>        * spring默认创建对象的时间：在创建spring容器时，会创建配置文件中的所有对象
>        * spring默认创建的是无参构造
>        */
>        
>         //1.指定配置文件路径
>         String config="bean.xml"; 
>         //2.创建容器
>         //创建容器的对象 ，ApplicationContext
>         //ClassPathXmlApplicationContext 从类路径中加载spring的配置文件
>         ApplicationContext applicationContext= new ClassPathXmlApplicationContext(config);
>         // 执行完上面这句代码就完成 创建对象
>         //从容器中获取某个对象
>         //applicationContext.getBean("配置文件的id");
>        // spring 在配置中创建对象 someservice
>        Someservice someservice= (Someservice) applicationContext.getBean("somecervice");
>        //使用spring创建好的对象
>         someservice.sode();
> ```
>
> 

#### 获取spring容器的对象信息

```java
 //1.指定配置文件路径
        String config="bean.xml";
        //创建容器的对象 ，ApplicationContext
        ApplicationContext applicationContext= new ClassPathXmlApplicationContext(config);
        //获取容器的对象的数量
        int b= applicationContext.getBeanDefinitionCount();
        System.out.println(b);
        //容器中自定义名称
        String  a[]=  applicationContext.getBeanDefinitionNames();
        for (String name:a){
            System.out.println(name);
        }
```

#### spring给java对象属性赋值





















