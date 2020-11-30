## Spring

#### IOC：控制反转(Inversion of Control)

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

> 1.Set方式注入（Setter Injection）（基本类型）[重要]
>
> ```java
>  <!--申明Student对象
>      <bean id="XX" class="XX">
>     <property name="属性名字" value="属性值"/>
>      </bean>
>        必须有set方法，否则会报错
>     -->
>     <bean id="mystudent" class="com.spring.wenqingwang.po.student">
>         <property name="age" value="21"/>
>         <property name="name" value="www"/>
>     </bean>
> ```
>
> 测试
>
> ```java
>  //构造方法先执行
> @Test
>     public  void  test01(){
>         String  path="applicationContext.xml";
>         ApplicationContext applicationContext= new ClassPathXmlApplicationContext(path);
>       student st= (student) applicationContext.getBean("mystudent");
>         System.out.println(st);
> 
>     }
> ```
>
> 1.2..Set方式注入（Setter Injection）（引用类型）[重要]
>
> ```java
>  <bean id="mystudent" class="com.spring.wenqingwang.po.student">
>         <property name="age" value="21"/>
>         <property name="name" value="www"/>
>         <property name="school" ref="myschool"/>
>     </bean>
>     <!--引用类型注入
>      <bean id="XX" class="XX">
>     <property name="属性名字" ref="bend的id（对象的名称）"/>
>      </bean>
>      <bean id="xx" class="xx">
>        <property name="属性名字" value="属性值"/>
>     </bean>
>     -->
>     <bean id="myschool" class="com.spring.wenqingwang.po.School">
>         <property name="name" value="清华大学"/>
>         <property name="address" value="北京"/>
>     </bean>
> ```
>
> 2.构造方法注入
>
> ```java
>  
>  public  student(String myname,int myage,School myschool){
>         System.out.println("有参构造方法执行========");
>         this.age=myage;
>         this.name=myname;
>         this.school=myschool;
>     }
> 
> <!--构造方法注入
>     构造注入使用 <constructor-arg />标签
>     name 构造方法的行参
>     index 构造方法的形参位置，从左往右
>     value 简单类型赋值
>     ref 引入类型赋值
>     -->
>     <bean id="mystudentgouzao" class="com.spring.wenqingwang.po.student">
>         <constructor-arg name="myage" value="21"/>
>         <constructor-arg name="myname" value="www"/>
>         <constructor-arg name="myschool" ref="myschool"/>
>     </bean>
>      <!--index位置 可以省略index 但是必须按照形参顺序 -->
>      <bean id="mystudentgouzao" class="com.spring.wenqingwang.po.student">
>         <constructor-arg index="0" value="www"/>
>         <constructor-arg index="1" value="26"/>
>         <constructor-arg index="2" ref="myschool"/>
>     </bean>
> ```
>
> 3.自动注入byName和byType
>
>  引用类型的自动注入：spring 框架根据某些规则可以给引用类型赋值，给引用类型赋值的规则常有，byName ，byType
>
> byname（按照名称注入）：Java类中引用类型的属性名和Spring容器的配置“id”名称一样，且数据类型一样，有这样的bean，spring可以赋值给引用类型
>
> 属性名与配置文件id一样如图
>
> ![属性名与配置文件id一样如图](https://i.loli.net/2020/11/30/fYGnAhZ5UCDO1Jj.png)
>
> 语法：
>
> ```
> <bean id="xx" class="xx"  autowire="byName"/>
> ```
>
> ```java
> <bean id="mystudent" class="com.spring.wenqingwang.po.student" autowire="byName">
>         <property name="age" value="21"/>
>         <property name="name" value="www"/>
>     </bean>
>     <bean id="school" class="com.spring.wenqingwang.po.School">
>         <property name="name" value="清大学"/>
>         <property name="address" value="北京"/>
>     </bean>
> ```
>
> byType（按类型注入）
>
> Java引用类型的数据类型和spring容器中（配置文件）bean 的class是同源关系，这样得可以赋值引用类型
>
> 1. java类中引用类型的数据类型和bean的class的值一样
> 2. java类中引用类型的数据类型和bean的class是父子类关系
> 3. java类中引用类型的数据类型bean的class值接口和实现关系
>
> 提醒：在byType中，在XMl配置文件中声明bean只能有一个符合条件的，多余一个就是错误的
>
> ```java
> <bean id="mystudent" class="com.spring.wenqingwang.po.student" autowire="byType">
>         <property name="age" value="21"/>
>         <property name="name" value="www"/>
>     </bean>
>     <bean id="myschol" class="com.spring.wenqingwang.po.School">
>         <property name="name" value="清大学"/>
>         <property name="address" value="北京"/>
>     </bean>
> ```

#### 包含配置文件

> 语法：
>
> ```java
> <import resource="classpath:其他配置文件的路径"/>
>  关键字："classpath" 表示类路径（class文件所在的目录）
>     在spring配置文件中要指定其他文件的位置，需要使用classpath，告诉spring在哪里读取
>  
> ```
>
> 通配符*
>
> ```java
> <import resource="classpath:*.xml"/>
> ```

#### spring注解

> 语法：
>
> 声明组件扫描器component-scan就是java对象
>
> component-scan工作方式：spring会扫描遍历base-package指定的包
>
> 把包中的所有的类，找到类中的注解，按照注解的功能创建对象或者属性赋值
>
> ```java
> <context:component-scan base-package="指定你注解的包名"/>
> ```
>
> 















