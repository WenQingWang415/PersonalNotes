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
> ![属性名与配置文件id一样如图](https://i.loli.net/2020/12/01/cRusJfyZBOVb2No.png)
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

##### byType（按类型注入）

> Java引用类型的数据类型和spring容器中（配置文件）bean 的class是同源关系，这样得可以赋值引用类型
>
> 1. java类中引用类型的数据类型和bean的class的值一样
>  2. java类中引用类型的数据类型和bean的class是父子类关系
>    3. java类中引用类型的数据类型bean的class值接口和实现关系
>    
>    提醒：在byType中，在XMl配置文件中声明bean只能有一个符合条件的，多余一个就是错误的
>    
>    ```java
>    <bean id="mystudent" class="com.spring.wenqingwang.po.student" autowire="byType">
>            <property name="age" value="21"/>
>            <property name="name" value="www"/>
>        </bean>
>     <bean id="myschol" class="com.spring.wenqingwang.po.School">
>        <property name="name" value="清大学"/>
>         <property name="address" value="北京"/>
>    </bean>
>    ```
> ```
> 
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
> 指定包的三种方式，第一种
> <context:component-scan base-package="指定你注解的包名"/>
> 指定包的三种方式，第二种 使用分割符(,或者;)分割多个包名
> <context:component-scan base-package="指定你注解的包名,指定你注解的包名"/>
> 指定包的三种方式，第三种 指定父包名  不建议使用
> <context:component-scan base-package="指定你注解的包名的上一级"/>
> ```
>

#####@Component

> ```java
>@Component
> public class student {
>}
> @Component(value = "mystudent") 等价于<bean id="mystudent" class="xx"/>
>可以简写：@Component("mystudent") //比较常用
> 可以省略：@Component 不指定名称，由spring提供默认名称，类名首字母小写
>然后指定扫描包路径
> <context:component-scan base-package="指定你注解的包名"/>
> ```
> 
> spring中和@Component注解功能一致的创建对象还有：
> 
> - @Repository（持久层） ：放在dao的实现类上面，表示创建dao对象，dao对象是访问数据库的。
> - @Service（业务层）：放在Service的实现类上面，创建Service对象，Service对象就是做业务处理，可以有事务功能等
> - @Controller（控制层）：放在Controller的控制器类上面，创建Controller对象，能够接受用户的处理参数，返回的结果
>
> 

##### @Value

> 语法：
>
> ```java 
> @Value("29")
> private  int age;
> ```
>
> ```java
> 简单类型属性赋值
> 属性：Value 是String类型的，表示简单类型赋值
> 位置： 在定义属性的上面，不需要set方法，推荐使用
>        在set方法上面
> @Value("赋值") 等价于  <property name="xx" value="xx"/>
> ```
>



#####@Autowired（自动注入，支持byName，byType）

> 枚举确定自动装配状态：即，bean是否应该使用setter注入由Spring容器自动注入其依赖项。@Autowired默认是按照类型装配注入的。这是Spring DI的核心概念。
>
>  默认使用byType注入
>
> 语法：
>
> ```java
>  @Autowired 
> private  School school;
> 然后对应的类加上@Component注解
> ```
>
> 等价于xml注入如图：
>
> ![](https://i.loli.net/2020/12/01/puMFrR2TqI4axbO.png)

#####@Autowired（byName注入） 需要配合@Qualifier("xx")注解使用

> @Autowired(required=false) ，如果我们想使用byName装配可以结合@Qualifier注解进行使用，如下：
>
> ```java
> @Autowired() 
> @Qualifier("baseDao")     
> private BaseDao baseDao;    
> ```
>
> 
>
> ![](https://i.loli.net/2020/12/01/VuIrxX1ycjkWCBQ.png)

#####@Resource(jdk中的注解)

> @Resource默认按照ByName自动注入，由J2EE提供，需要导入包javax.annotation.Resource。@Resource有两个重要的属性：name和type，而Spring将@Resource注解的name属性解析为bean的名字，而type属性则解析为bean的类型。所以，如果使用name属性，则使用byName的自动注入策略，而使用type属性时则使用byType自动注入策略。如果既不制定name也不制定type属性，这时将通过反射机制使用byName自动注入策略。
>
> ```java 
> public class TestServiceImpl {
>     // 下面两种@Resource只要使用一种即可
>     @Resource(name="userDao")
>     private UserDao userDao; // 用于字段上
>     
>     @Resource(name="userDao")
>     public void setUserDao(UserDao userDao) { // 用于属性的setter方法上
>         this.userDao = userDao;
>     }
> }
> ```
>
> 
>
> @Resource装配顺序：
>
> ①如果同时指定了name和type，则从Spring上下文中找到唯一匹配的bean进行装配，找不到则抛出异常。
>
> ②如果指定了name，则从上下文中查找名称（id）匹配的bean进行装配，找不到则抛出异常。
>
> ③如果指定了type，则从上下文中找到类似匹配的唯一bean进行装配，找不到或是找到多个，都会抛出异常。
>
> ④如果既没有指定name，又没有指定type，则自动按照byName方式进行装配；如果没有匹配，则回退为一个原始类型进行匹配，如果匹配则自动装配。
>
> @Resource的作用相当于@Autowired，只不过@Autowired按照byType自动注入。
>
> ![](https://i.loli.net/2020/12/01/FtcxHmNsTQ34gq7.png)

#### AOP面向切面编程

> AOP面向切面编程是基于动态代理的，可以使用 JDK动态代理，也可以使用GGLIB动态代理
>
> AOP其实就是让动态代理规范化，把动态代理的实现步骤，方式都定义好了，让开发人员用一种方式，是使用动态代理

##### 动态代理

> - JDK动态代理（通过接口） ：实现JDK中``Proxy``，``Method``，InvocationHandler 创建代理对象
> - GGLIB动态代理（通过继承）：第三方工具库，通过继承目标类，创建子类，子类是代理的对象，目标方法和类不能是FInal的
>
> 

##### 术语

> - Aspeot ：切面，表示增强的功能，是一堆代码，完成某个功能，不是业务代码
>
> 常见的切面：日志，事务，权限，统计，参数检查
>
> - Joinpoint：连接点，连接页面和切面的位置，就某类的业务的方法
>
> - PointCut：切入点，连接点方法的集合，多个方法
>
> - 目标对象：给那个类添加功能，这个类就是目标对象
>
> - Advice:通知，通知切面执行的时间
>
>   切面有三关键的要素
>
>   1. 切面的功能代码，切面能干什么
>   2. 切面执行的位置，使用Pointout切面执行的位置
>   3. 切面执行的时间，使用Advice表示时间，在目标方法之前，还在目标方法之前

##### AOP的实现

> AOP是一个规范，是动态化的一个规范，一个标准

#####AOP技术实现框架：

> 1. spring :spring内部实现了AOP规范，能做AOP的工作，Spring主要在事务使用Aop，在项目中很少使用spring的AOP实现，SPring的AOP比较麻烦，笨重
>
> 2.Aspectj: 是一个开源专门做AOP的框架，Spring框架中集成了Aspectj框架，通过spring就可以使用Aspectj功能

#####Aspectj框架有两种实现方式：

> 1. 使用Xml方式
>
> 2. 使用注解方式，在项目中一般使用注解方式
>
>    Aspectj有五种注解：
>
>    1. @Before: 前置通知, 在方法执行之前执行
>    2. @After: 后置通知, 在方法执行之后执行 。
>    3. @AfterRunning: 返回通知, 在方法返回结果之后执行
>    4. @AfterThrowing: 异常通知, 在方法抛出异常之后
>    5. @Around: 环绕通知, 围绕着方法执行

##### Aspectj切点表达式：

> 采用`execution`关键字定义的切点表达式格式如下：
>
> ```java
> execution(modifiers-pattern? ret-type-pattern declaring-type-pattern?name-pattern(param-pattern)
>                 throws-pattern?)
> ```
>
> 表达式中除了返回值类型匹配规则`ret-type-pattern` (通常是 *来匹配所有返回值类型)之外的其他类型匹配规则都是可选的
>
> `name-pattern`方法名，可以是具体的方法名，也可以用*圈定所有方法
>
> `param-pattern`方法入参：`（）`匹配无参方法，`(..)`匹配多参数方法，`（*）`匹配单参数任意入参类型的方法，`(*,String)`匹配有两个入参的方法，第一个可以是任意类型，第二个必须是字符串类型。
>
> ```java
> execution(public * *(..)) //匹配所有public方法
> execution(* set*(..))//匹配所有方法名开头为set的方法
> execution(* com.xyz.service.AccountService.*(..))//匹配AccountService下的所有方法
> execution(* com.xyz.service.*.*(..))//匹配service包下的所有方法
> execution(* com.xyz.service..*.*(..))//匹配service包或其子包下的所有方法
> within(com.xyz.service.*)//匹配service包下的所有方法
> within(com.xyz.service..*)//匹配service包或其子包下的所有方法
> this(com.xyz.service.AccountService)//匹配所有实现了AccountService接口的类的代理类的方法（注意是代理类）
> target(com.xyz.service.AccountService)//匹配所有实现了AccountService接口的类的方法（注意是本类）
> args(java.io.Serializable)//匹配只有一个入参，且入参实现了Serializable接口的方法
> @target(org.springframework.transaction.annotation.Transactional)//匹配类上标注了@Transactional注解的类中方法
> @within(org.springframework.transaction.annotation.Transactional)//匹配运行时子类上标注了@Transactional注解的类中方法
> @annotation(org.springframework.transaction.annotation.Transactional)//匹配所有打了@Transactional注解的方法
> @args(com.xyz.security.Classified)//匹配只有一个入参，且运行时入参有@Classified注解的方法
> bean(tradeService)//匹配命名为tradeService的类的方法
> bean(*Service)//匹配命名后缀为Service的类的方法
> ```



#####Aspectj的使用步骤：

> - 引入依赖项
>
> ```java
> <dependency>
>     <groupId>org.springframework</groupId>
>     <artifactId>spring-aspects</artifactId>
>     <version>5.3.1</version>
> </dependency>
> ```
>
> - 创建目标类和实现类：给类中的方法添加功能
>
> ```java
> //接口：
>     public interface Some01 {
>     void  some(String name,int age);
> }
> //实现类： 
> //目标类
> /**
> *@Component 不需要写xml
> */
> @Component
> public class Some01Impl implements Some01 {
>     @Override
>     public void some(String name, int age) {
>         System.out.println("=========目标执行方法some()========");
>     }
> }
> ```
>
> - 创建切面的普通类
>
>   1. 在类上添加 @Aspect
>
>   2. 在类中定义方法，方法就是切面要执行的功能代码
>
>      在方法上面添加Aspect注解的通知注解
>
>      ```java
>      /**
>       * @Aspect 是Aspectj中的注解
>       * 作用：表示当前是切面类
>       * 切面类：是给业务类方法添加功能，在这个中有切面的功能代码
>       */
>      @Component
>      @Aspect
>      public class myAspectj {
>          /**
>           * 定义方法：方法实现切面功能
>           * 方法定义的要求：
>           * 1.公共方法：public
>           * 2.方法没有返回值
>           * 3.方法名称自定义
>           * 4.方法可以有参数，也可以没有参数
>           *   如果有参数，参数不是自定义的，有几个参数类型可以使用
>           *
>           */
>          /**
>           * @Before: 前置通知
>           * 属性：value，是切入点表达式，表示切面执行的位置
>           * 位置：在方法的上面添加
>           * 特点：
>           * 1.在目标方法之前执行
>           * 2.不会改变目标的执行结果
>           * 3.不影响目标方法的执行
>           */
>          @Before(value ="execution(public void  com.spring.wenqingwang.service.be01.Some01Impl.some(String,int))")
>          public  void myBefore(){
>              //就是切面要执行的功能代码
>              System.out.println("切面功能，在目标方法之前输出执行时间"+new Date());
>          }
>          =================================分割简写方式如下=====================
>          @Before(value ="execution( void  com.spring.wenqingwang.service.be01.Some01Impl.some(String,int))")
>          public  void myBefore(){
>              //就是切面要执行的功能代码
>              System.out.println("切面功能，在目标方法之前输出执行时间"+new Date());
>          }
>           =================================分割简写方式如下=====================
>          @Before(value ="execution( void  *..Some01Impl.some(String,int))")
>          public  void myBefore(){
>              //就是切面要执行的功能代码
>              System.out.println("03s切面功能，在目标方法之前输出执行时间"+new Date());
>          }
>            =================================分割简写方式如下=====================
>          @Before(value ="execution( void  *..Some01Impl.some(..))")
>          public  void myBefore(){
>              //就是切面要执行的功能代码
>              System.out.println("04切面功能，在目标方法之前输出执行时间"+new Date());
>          }
>           =================================分割简写方式如下=====================
>           @Before(value ="execution( *  *..Some01Impl.some(..))")
>          public  void myBefore(){
>              //就是切面要执行的功能代码
>              System.out.println("05切面功能，在目标方法之前输出执行时间"+new Date());
>          }
>           =================================分割简写方式如下=====================
>          @Before(value ="execution( *  *..Some01Impl.so*(..))")
>          public  void myBefore(){
>              //就是切面要执行的功能代码
>              System.out.println("06切面功能，在目标方法之前输出执行时间"+new Date());
>          }
>           =================================分割简写方式如下=====================
>          @Before(value ="execution( *  so*(..))")
>          public  void myBefore(){
>              //就是切面要执行的功能代码
>              System.out.println("07切面功能，在目标方法之前输出执行时间"+new Date());
>          }
>      ```
>
> - 创建spring配置文件:声明对象，把对象交个容器统一管理，声明对象可以使用注解或者xml文件<bean/>
>
>   1. 声明目标对象
>   2. 声明切面对象
>   3. 声明Aspectj框架中自动代理生成器标签
>
>   ```java
>     <!--声明组件扫描器-->
>   <context:component-scan base-package="com.spring.wenqingwang.service.be01"/>
>       <!--声明自动代理生成器，使用 Aspectj的内部功能，创建目标代理对象，
>       创建目标代理对象是在内存中实现的，修改目标对象在内存的结构，创建为代理对象，所以目标对象是修改后的代理对象
>       aspectj-autoproxy 会把spring容器中的所有的目标对象，一次性都生成代理对象-->
>       <aop:aspectj-autoproxy/>
>   ```
>
>   如图：
>
>   ![](https://i.loli.net/2020/12/02/scrieb8GpWX6JS1.png)
>
> - 测试
>
>   ```java
>   @Test
>       public  void  test02(){
>           String path="zhujie.xml";
>           ApplicationContext applicationContext=new ClassPathXmlApplicationContext(path);
>           //从容中获取目标对象
>            Some01 some01ome01= (Some01) applicationContext.getBean("some01Impl");
>            //通过代理对象执行方法，实现目标方法执行时，增强功能
>           some01ome01.some("www",20 );
>       }
>   ```
>
> 
>
> 

#####Joinpoint通知方法中的参数：

==所有的通知都可使用JoinPoint 必须是第一个位置的参数==

> ```
> /**
>      * 指定通知中的参数：JoinPoint
>      * JoinPoint：业务方法，添加要切入的功能的业务方法
>      * 作用：可以在通知方法获取执行时的信息，列如方法名称，方法的实参，
>      * 如果方法要使用到方法信息就加入JoinPoint
>      * 这个JoinPoint参数是由框架赋予的，必须是第一个位置的参数
>      *
>      */
>     @Before(value ="execution( void  *..Some01Impl.some(..))")
>     public  void myBefore(JoinPoint joinPoint){
>         //获取方法的完整定义
>         System.out.println("方法的签名（定义）"+joinPoint.getSignature());
>         System.out.println("方法的名称="+joinPoint.getSignature().getName());
>         //获取实参
>         Object a []=joinPoint.getArgs();
>         for (Object as:a){
>             System.out.println("参数"+as);
>         }
>         //就是切面要执行的功能代码
>         System.out.println("07切面功能，在目标方法之前输出执行时间"+new Date());
>     }
> ```



#####后置通知 @AfterRunning

>  声明接口
>
> ```java
> public interface dosome {
>     String some(String name,int age);
> }
> ```
>
> 实现接口
>
> ```java
> @Component
> public class dosomeImpl implements dosome {
>     @Override
>     public String some(String name, int age) {
>         System.out.println("==========SOme目标后通知===========");
>         return "ADCDEFG";
>     }
> }
> ```
>
> 写切面
>
> ```java
> @Component
> @Aspect
> public class MyAfterRunning {
>     /***
>      * 后置通知定义实现方法
>      * 方法定义的要求：
>      *      * 1.公共方法：public
>      *      * 2.方法没有返回值
>      *      * 3.方法名称自定义
>      *      * 4.方法有参数的 参数推荐使用Object
>      * @param res
>      */
>     /***
>      * @AfterReturning后置通知
>      * 属性：value：切入点表达式
>      *      returning 自定义变量，表示目标方法的返回值
>      *      自定义的变量必须和通知方法的形参名一样
>      * 特点：
>      * 1.在目标方法之后执行的
>      * 2.能够获取目标的返回值，可以根据这个返回值处理不同的功能
>      * 3.可以修改返回值
>      * @param res
>      */
>     @AfterReturning(value = "execution(* *..dosomeImpl.some(..))",returning = "res")
>     public  void  myafterRunning(Object res){
>         //Object res 是目标执行后的返回值，根据返回值做切面功能的处理
>         System.out.println("后置通知，在方法后通知"+res);
>     }
> }
> ```
>
> xml扫描组件
>
> ```java
> <!--声明组件扫描器-->
> <context:component-scan base-package="com.spring.wenqingwang.service.be02"/>
> <!--声明自动代理生成器，使用 Aspectj的内部功能，创建目标代理对象，
> 创建目标代理对象是在内存中实现的，修改目标对象在内存的结构，创建为代理对象，所以目标对象是修改后的代理对象
> aspectj-autoproxy 会把spring容器中的所有的目标对象，一次性都生成代理对象-->
> <aop:aspectj-autoproxy/>
> ```
>
> 然后进行测试
>
> ```java
> @Test
> public  void  test02(){
>     String path="zhujie.xml";
>     ApplicationContext applicationContext=new ClassPathXmlApplicationContext(path);
>     //从容中获取目标对象
>      dosome peoxy= (dosome) applicationContext.getBean("dosomeImpl");
>  String str=peoxy.some("wwwq",25);
>     System.out.println(str);
> }
> ```
>
> ![image.png](https://i.loli.net/2020/12/02/XVDN9LhdkzruHCi.png)
>
> 
>

##### 环绕通知 @Around

> 声明接口
>
> ```java
> public interface Some03 {
>     String some(String name,int age);
> }
> 
> ```
>
> 声明目标类
>
> ```java
> @Component
> public class Some03Impl implements Some03 {
>     @Override
>     public String some(String name, int age) {
>         System.out.println("环绕通知执行了");
>         return "就这";
>     }
> }
> 
> ```
>
> 写切面
>
> ```java
> @Component
> @Aspect
> public class Myaspct {
>     /**
>      * 环绕通知方法定义格式
>      * 1.public
>      * 2.必须有一个返回值 推荐使用Object
>      * 3.方法名称自定义
>      * 4.方法有参数，固定参数ProceedingJoinPoint
>      */
>     /**
>      * @Around :环绕通知
>      * 属性：value 切入点表达式
>      * 特点：
>      * 1.功能最强的通知
>      * 2.在目标方法前后都能增强功能
>      * 3.控制目标方法是否被调用执行
>      * 4.修改原来的目标方法执行结果，影响最后的调用结果
>      * 环绕通知，等同于jdk动态代理的InvocationHandler
>      * 参数：ProceedingJoinPoint 等同于jdk动态代理的``Method``
>      * 作用：执行目标方法
>      * 返回值：目标返回的结果，可以被修改
>      *
>      * 环绕通知做的最多就是事务
>      */
>     @Around(value = "execution(* *..Some03Impl.some(..))")
>     public Object MyAuround(ProceedingJoinPoint point) throws Throwable {
>         Object object = null;
>         String name = null;
>         Object args[] = point.getArgs();
>         if (args != null) {
>             Object agr = args[0];
>             name = (String) agr;
>         }
>         System.out.println("环绕通知：在目标方法之前，输出时间" + new Date());
>         //1.目标方法的调用 object 目标返回的结果
>          //控制目标方法是否被调用执行
>         if (name.equals("wwwq")) {
>             object = point.proceed();//Method.invoke();
>         }
>         System.out.println("环绕通知：在目标方法之后，提交事务");
>         //在目标方法的前或者后加入功能
>         //修改返回结果
>         if (object!=null){
>             object="wang";
>         }
>         //返回通知
>         return object;
> 
>     }
> }
> 
> ```
>
> xml扫描组件
>
> ```java
> <!--声明组件扫描器-->
>     <context:component-scan base-package="com.spring.wenqingwang.service.be03"/>
>     <!--声明自动代理生成器，使用 Aspectj的内部功能，创建目标代理对象，
>     创建目标代理对象是在内存中实现的，修改目标对象在内存的结构，创建为代理对象，所以目标对象是修改后的代理对象
>     aspectj-autoproxy 会把spring容器中的所有的目标对象，一次性都生成代理对象-->
>     <aop:aspectj-autoproxy/>
> ```
>
> 测试：
>
> ```java
>  @Test
>     public  void  test02(){
>         String path="zhujie.xml";
>         ApplicationContext applicationContext=new ClassPathXmlApplicationContext(path);
>         //从容中获取目标对象
>         Some03 peoxy= (Some03) applicationContext.getBean("some03Impl");
>      String str=peoxy.some("wwwq",25);
>         System.out.println(str);
>     }
> ```

##### 异常通知@AfterThrowing（了解即可）

>  声明接口
>
> ```java
> void  dosene();
> ```
>
> 声明目标实现类
>
> ```java
> @Override
>     public void dosene() {
>         System.out.println("异常通知"+1/0);
>     }
> ```
>
> 切面
>
> ```java
> @Component
> @Aspect
> public class Myaspct {
>     /**
>      * 异常通知方法定义格式
>      * 1.public
>      * 2.没有返回值
>      * 3.方法名称自定义
>      * 4.方法有一个Exception，如果还要有的话就是JoinPoint
>      *
>      */
>     /**
>      * @AfterThrowing:异常通知 属性：
>      * value 切入点表达式
>      * throwing：自定义变量，表示目标方法抛出的异常对象
>      * 变量名必须和方法名一样
>      * 特点：
>      * 1.在目标方法抛出异常是执行的
>      * 2.可以做异常的监控程序，监控目标方法执行是不是有异常，如果有异常可以可以发送邮件，短信进行通知
>      */
>     @AfterThrowing(value = "execution(* *..Some03Impl.dosene(..))", throwing = "e")
>     public void yichang(Exception e) {
>         System.out.println("异常通知：在方法发生异常是通知");
>     }
> }
> 
> ```
>
> xml配置
>
> ```java
>   <!--声明组件扫描器-->
>     <context:component-scan base-package="com.spring.wenqingwang.service.be04"/>
>     <!--声明自动代理生成器，使用 Aspectj的内部功能，创建目标代理对象，
>     创建目标代理对象是在内存中实现的，修改目标对象在内存的结构，创建为代理对象，所以目标对象是修改后的代理对象
>     aspectj-autoproxy 会把spring容器中的所有的目标对象，一次性都生成代理对象-->
>     <aop:aspectj-autoproxy/>
> ```
>
> 测试
>
> ```java
> @Test
>     public  void  test02(){
>         String path="zhujie.xml";
>         ApplicationContext applicationContext=new ClassPathXmlApplicationContext(path);
>         //从容中获取目标对象
>         Some03 peoxy= (Some03) applicationContext.getBean("some03Impl");
>         peoxy.dosene();
>     }
> ```

##### 最终通知@After（了解即可）

> 接口
>
> ```java
>  void doAfter();
> ```
>
> 目标实现类
>
> ```java
>  @Override
>     public void doAfter() {
>         System.out.println("最终通知"+1/0);
>     }
> ```
>
> 切面
>
> ```java
> @Component
> @Aspect
> public class Myaspct {
>     /**
>      * 异常通知方法定义格式
>      * 1.public
>      * 2.没有返回值
>      * 3.方法名称自定义
>      * 4.方法没有参数，如果还要有的话就是JoinPoint
>      *
>      */
>     /**
>      * @After ：最终通知
>      * 属性：
>      * value 切入点表达式
>      * 特点：
>      * 1.在目标方法之后执行
>      * 2.总会执行
>      *一般做内存清除
>      */
>     @After(value = "execution(* *..Some03Impl.doAfter(..))")
>     public  void dovAfter(){
>     System.out.println("切面执行了");
> }
> }
> 
> ```
>
> xml扫描器
>
> ```java
> <!--声明组件扫描器-->
>     <context:component-scan base-package="com.spring.wenqingwang.service.be05"/>
>     <!--声明自动代理生成器，使用 Aspectj的内部功能，创建目标代理对象，
>     创建目标代理对象是在内存中实现的，修改目标对象在内存的结构，创建为代理对象，所以目标对象是修改后的代理对象
>     aspectj-autoproxy 会把spring容器中的所有的目标对象，一次性都生成代理对象-->
>     <aop:aspectj-autoproxy/>
> ```
>
> 测试
>
> ```java
> @Test
>     public  void  test02(){
>         String path="zhujie.xml";
>         ApplicationContext applicationContext=new ClassPathXmlApplicationContext(path);
>         //从容中获取目标对象
>         Some03 peoxy= (Some03) applicationContext.getBean("some03Impl");
>         peoxy.doAfter();
>     }
> ```



##### PointCut 的注解

> ```java
> @Component
> @Aspect
> public class Myaspct {
> 
>     @After(value = "mypt()")
>     public  void dovAfter(){
>     System.out.println("在方法后执行了");
> }
>     @Before(value = "mypt()")
>     public  void dovbfter(){
>         System.out.println("在方法前执行了");
>     }
> /***
>  * @Pointcut:定义和管理切入点，如果项目中有多个切入点是重复的，可以复用的可以使用 @Pointcut
>  * 属性：value 切入点表达式
>  * 特点：当使用@Pointcut定义在一个方法上面，此方法的名称是切入点表达式的别名
>  * 其他的通知中，value属性就可以使用方法名称，代替切入点表达式
>  */
> @Pointcut(value = "execution(* *..Some03Impl.doAfter(..))")
> public  void mypt(){
>     //不需要代码
> }
> ```

##### 使用Cglib代理

> ```java
> <!--如果你是的期望是Cglib代理 expose-proxy="true" 告诉框架使用Cglib代理-->
>     <aop:aspectj-autoproxy expose-proxy="true"/>
>  //没有接口是cglib代理
> ```

#### Druid连接池使用：阿里巴巴开源的数据库连接池项目

[Druid连接池](https://github.com/alibaba/druid)

#### spring的事务处理

##### 什么是事务：

> 事务是指一组SQL语句的集合，集合中有多个SQL语句 insert select update  delete ,我们希望语句都成功或者失败，这些SQL语句是一个整体，

##### 什么时候使用事务

> 涉及到多个表或者多个SQL语句，保证这些语句成功，保证操作都符合要求

##### Spring声明式事务

> 把事物相关的资源和内容都提供给spring，spring就可以处理事务的提交和回滚
>
> 1. 事务内部提交，回滚事务，使用的事务管理器对象，代替你完成commit，rollback
>
>    事务管理器是一个接口和他众多的实现类
>
>    接口：PlatformTransactionManager  定义了事务的重要方法：commit，rollback
>
>    实现类：spring把每一种数据库访问技术对应的事务处理类都创建好
>
>    ​                 mybatis访问数据库---spring创建的事务[DataSourceTransactionManager](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/datasource/DataSourceTransactionManager.html)
>
>    ​                Hibernate访问数据库---spring创建事务[HibernateTransactionManager](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/orm/hibernate5/HibernateTransactionManager.html)

##### 控制事务的三个方面

###### 事务的隔离级别：

> [ISOLATION_DEFAULT](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#ISOLATION_DEFAULT)：PlatfromTransactionManager默认的事务隔离级别。mySQL为[ISOLATION_REPEATABLE_READ](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#ISOLATION_REPEATABLE_READ)，oracle为[ISOLATION_READ_COMMITTED](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#ISOLATION_READ_COMMITTED)
>
> [ISOLATION_READ_COMMITTED](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#ISOLATION_READ_COMMITTED)：读已提交，解决脏读，存在不可重复读和幻读
>
> [ISOLATION_READ_UNCOMMITTED](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#ISOLATION_READ_UNCOMMITTED)：最低的隔离级别，读未提交，未解决任何并发的问题
>
> [ISOLATION_REPEATABLE_READ](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#ISOLATION_REPEATABLE_READ)：可重复读，解决脏读，不可重复读，存在幻读
>
> [ISOLATION_SERIALIZABLE](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#ISOLATION_SERIALIZABLE)：串行化，不存在并发问题
>
> 关键词：
>
> 1. 脏读：脏读是指当一个事务在访问数据时，并且对数据进行了修改，而这种修改还没有存在数据库中，这时，另一个事务访问这个数据，然后使用这个数据
> 2. 不可重复读：是指一个事务内，多次读同一条数据，但是这个事务还木结束是，另一个事务也访问同一数据，么，在第一个事务中的两 次读数据之间，由于第二个事务的修改，那么第一个事务两次读到的的数据可能是不一样的。这样就发生了在一个事务内两次读到的数据是不一样的，因此称为是不 可重复读。
> 3. 幻读：是指当事务不是独立执行时发生的一种现象，例如第一个事务对一个表中的数据进行了修改，这种修改涉及到表中的全部数据行。 同时，第二个事务也修改这个表中的数据，这种修改是向表中插入一行新数据。那么，以后就会发生操作第一个事务的用户发现表中还有没有修改的数据行，就好象 发生了幻觉一样。例如，一个编辑人员更改作者提交的文档，但当生产部门将其更改内容合并到该文档的主复本时，发现作者已将未编辑的新材料添加到该文档中。 如果在编辑人员和生产部门完成对原始文档的处理之前，任何人都不能将新材料添加到文档中，则可以避免该问题。

###### 事务的的超时时间：

> [TIMEOUT_DEFAULT](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#TIMEOUT_DEFAULT)表示一个方法最长的执行时间，如果方法执行是超过时间，事务就回滚，单位为秒，默认是-1 。一般都是默认即可

###### 事务的传播行为：

> 控制业务是不是有事务，是什么样的事务
>
> 7个传播行为，表示你的业务方法调用时，事务在方法之间是如何使用的
>
> [PROPAGATION_REQUIRED](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_REQUIRED)：
>
> 如果存在一个事务，则支持当前事务。如果没有事务则开启一个新的事务。 这种传播行为最长见，是spring的默认传播行为
>
> [PROPAGATION_REQUIRES_NEW](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_REQUIRES_NEW)：
>
> 总是开启一个新的事务。如果一个事务已经存在，则将这个存在的事务挂起。
>
> [PROPAGATION_SUPPORTS](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_SUPPORTS):
>
> 如果存在一个事务，支持当前事务。如果没有事务，则非事务的执行。
>
> ------
>
> 以上三种经常使用
>
> [PROPAGATION_MANDATORY](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_MANDATORY)：
>
> 级别的事务要求上下文中必须要存在事务，否则就会抛出异常！配置该方式的传播级别是有效的控制上下文调用代码遗漏添加事务控制的保证手段。比如一段代码不能单独被调用执行，但是一旦被调用，就必须有事务包含的情况，就可以使用这个传播级别。
>
> [PROPAGATION_NESTED](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_NESTED)：
>
> 如果一个活动的事务存在，则运行在一个嵌套的事务中. 如果没有活动事务, 则按TransactionDefinition.PROPAGATION_REQUIRED 属性执行
>
> 事务是逻辑处理原子性的保证手段，通过使用事务控制，可以极大的避免出现逻辑处理失败导致的脏数据等问题。
>
> 事务最重要的两个特性，是事务的传播级别和数据隔离级别。传播级别定义的是事务的控制范围，事务隔离级别定义的是事务在数据库读写方面的控制范围。
>
> [PROPAGATION_NEVER](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_NEVER)：
>
> 该事务更严格，上面一个事务传播级别只是不支持而已，有事务就挂起，而PROPAGATION_NEVER传播级别要求上下文中不能存在事务，一旦有事务，就抛出runtime异常，强制停止执行！这个级别上辈子跟事务有仇。
>
> [PROPAGATION_NOT_SUPPORTED](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_NOT_SUPPORTED)：
>
> 这个也可以从字面得知，not supported ，不支持，当前级别的特点就是上下文中存在事务，则挂起事务，执行当前逻辑，结束后恢复上下文的事务。
>
> 这个级别有什么好处？可以帮助你将事务极可能的缩小。我们知道一个事务越大，它存在的风险也就越多。所以在处理事务的过程中，要保证尽可能的缩小范围。比如一段代码，是每次逻辑操作都必须调用的，比如循环1000次的某个非核心业务逻辑操作。这样的代码如果包在事务中，势必造成事务太大，导致出现一些难以考虑周全的异常情况。所以这个事务这个级别的传播级别就派上用场了。用当前级别的事务模板抱起来就可以了。

##### 事务提交事务，回滚事务的时机

> 1. 当你的业务方法，执行成功，没有抛出异常，当方法执行完毕，spring在方法执行后提交方法 ，事务管理器commit
>
> 2. 当你的业务方法抛出运行时异常或者ERROR的时候，spring执行回滚，事务管理器rollback
>
>    运行时异常的定义：RuntimeException 和他子类运行是的异常，列如：NullPoinException等异常
>
> 3. 当你的业务方法抛出非运行时异常，主要是受查异常时，提交事务。
>
>    受查异常：在你写代码中，必须处理的异常，例如：IOException，SQLException



