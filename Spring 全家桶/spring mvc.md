## spring  mvc



#### 简介：



> `spring mvc`是`spring`框架的一个模块，`spring`和`spring mvc`不需要中间件整合
>
> `spring mvc`是基于`mvc`的架构web框架
>
> `spring mvc`框架是一个基于请求驱动的web框架，使用了前端控制模式来设计，再根据请求映射规定分发相应的后端控制器进行处理

#### 请求处理流程

![image.png](https://i.loli.net/2020/12/12/uQ9tBREJw6aoG7F.png)

对工作原理的解释说明：

1. 用户发送请求到`spring mvc`框架提供的`DispatcherServlet `这个**前端控制器**

2. 前端控制器会去找处理映射器（`HandlerMapping`),处理映射器根据请求url找到具体的**后端控制器**（`Handler`），生成处理器对象以及处理器拦截器（如果有生成）一并返回`DispatcherServlet `

3. 根据处理映射器返回的后端控制器（`Handler`），`DispatcherServlet `会找合适的**处理器适配器**（`HandlerAdapter`）

4. **处理器适配器**`HandlerAdapter`会去执行后端控制器（Handler开发的时候被叫Controller也叫**后端控制器**），执行之前会有转换器，数据绑定，校验器等完成上面这些才会去真正的去执行Handler

5. **后端控制器**Handler执行完成之后返回一个ModelAndView对象

6. **处理器适配器**`HandlerAdapter`会将这个`ModelAndView`返回前端控制器`DispatcherServlet `前端控制器会将`ModelAndView`对象交给视图解析器`ViewResolve`

7. 视图解析器`ViewResolve`解析`ModelAndView`对象之后返回逻辑视图

8. 前端控制器`DispatcherServlet `对逻辑视图进行渲染（数据填充）之后返回真正的物理View并响应给浏览器

    



#### 入门开发环境

> 第一步：选择maven项目
>
> ![image.png](https://i.loli.net/2020/12/11/i2CEazy3k61bg4m.png)
>
> 第二步：填写项目名字以及路径
>
> ![image.png](https://i.loli.net/2020/12/11/aGhlIP7ZTjAsU3R.png)
>
> 第三步：选择自己安装的maven以及配置
>
> ![image.png](https://i.loli.net/2020/12/11/IamhZcOWU3fzMPl.png)
>
> 第四步：补全目录
>
> ![image.png](https://i.loli.net/2020/12/11/Wyts9xrIivPZouC.png)
>
> 

##### pom.xml

> ```xml
> <properties>
>         <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
>         <maven.compiler.source>1.8</maven.compiler.source>
>         <maven.compiler.target>1.8</maven.compiler.target>
>         <spring.version>5.2.6.RELEASE</spring.version>
>     </properties>
> 
>     <dependencies>
>         <dependency>
>             <groupId>junit</groupId>
>             <artifactId>junit</artifactId>
>             <version>4.11</version>
>             <scope>test</scope>
>         </dependency>
>         <!--spring-webmvc 包含spring-aop，context，core，web，expression，beans-->
>         <dependency>
>             <groupId>org.springframework</groupId>
>             <artifactId>spring-webmvc</artifactId>
>             <version>${spring.version}</version>
>         </dependency>
> 
>         <!--java web begin-->
>         <dependency>
>             <groupId>javax.servlet</groupId>
>             <artifactId>javax.servlet-api</artifactId>
>             <version>4.0.1</version>
>         </dependency>
>         <dependency>
>             <groupId>javax.servlet</groupId>
>             <artifactId>jstl</artifactId>
>             <version>1.2</version>
>         </dependency>
>         <dependency>
>             <groupId>javax.servlet.jsp</groupId>
>             <artifactId>jsp-api</artifactId>
>             <version>2.0</version>
>         </dependency>
>         <!--java web end-->
>     </dependencies>
> ```
>
> 

##### 添加web.xml头

> ```xml
> <web-app xmlns="http://java.sun.com/xml/ns/javaee"
>          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>          xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
>          version="3.0">
>   <display-name>Archetype Created Web Application</display-name>
> </web-app>
> ```
>
> **或者在IDea设置**
>
> ![image.png](https://i.loli.net/2020/12/12/5x3iGYEZBWgHR2p.png)

##### 在src/main/resources创建spring-config.xml

> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <beans xmlns="http://www.springframework.org/schema/beans"
>        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>        xsi:schemaLocation="http://www.springframework.org/schema/beans
>        http://www.springframework.org/schema/beans/spring-beans.xsd">
> 
> </beans>
> ```

##### 在web.xml配置UTF-8编码

> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
>          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>          xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
>          version="4.0">
>     <!--配置字符集编码过滤器-->
>     <filter>
>         <filter-name>CharacterEncodingFilter</filter-name>
>         <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
>         <init-param>
>             <param-name>encoding</param-name>
>             <param-value>UTF-8</param-value>
>         </init-param>
>         <init-param>
>             <param-name>forceEncoding</param-name>
>             <param-value>true</param-value>
>         </init-param>
>     </filter>
>     <filter-mapping>
>         <filter-name>CharacterEncodingFilter</filter-name>
>         <url-pattern>/*</url-pattern>
>     </filter-mapping>
> </web-app>
> ```

##### 配置前端控制器 在web.xml

> ```xml
> <!--DispatcherServlet 配置前端控制器 servlet-->
>     <servlet>
>         <servlet-name>dispatcherServlet</servlet-name>
>         <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
>         <!--contextConfigLocation :指定spring mvc配置加载的位置
>    如果不指定则默认加载 WEB-INF/**-servlet.xml(例如：springmvc-serlet.xml)
>     -->
>         <init-param>
>             <param-name>contextConfigLocation</param-name>
>             <param-value>classpath:spring-config.xml</param-value>
>         </init-param>
>     </servlet>
>     <servlet-mapping>
>         <servlet-name>dispatcherServlet</servlet-name>
>         <!--可以拦截两种请求
>             第一种： 拦截固定后缀的URL，比如设置为*.do,*.action
>                     例如：/user/add.action 此方法比较简单，不会导致静态资源（jsp，js，css）被拦截
>             第二种：设置拦截所有 /
>                  例如：/user/add/ user/add.action此方法可以实现REST风格的url
>                       很多互联网类型应用使用这种方式
>                       但是此方法会导致静态资源（jsp，js，css）被拦截，需要特殊处理
>             错误设置：拦截所有，设置为/*
>         -->
>         <url-pattern>/</url-pattern>
>     </servlet-mapping>
> 
> ```
>
> 在src/main/resources/spring-config.xml配置适配器和处理器映射器==(可以不配)==
>
> ```xml
>     <!--处理器映射器-->
>     <!--根据后端的bean的name进行查找后端处理器，将请求的url配置在bean的name中-->
>     <!--这是默认的映射处理器可以不用配置-->
>     <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
>     <!--`HandlerAdapter`适配器-->
>     <!--这个也是默认的也可以不配置-->
>     <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
> ```

##### 设置后端控制器 Controller

> 开发Controller需要实现`import org.springframework.web.servlet.mvc.Controller`
>
> ```java
> 
> public class HelloController implements Controller {
> 
>     @Override
>     public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
> 
>         ModelAndView modelAndView = new ModelAndView();
>         //设置数据到模型
>         modelAndView.addObject("hello","spring mvc");
>         //设置逻辑视图路径
>         modelAndView.setViewName("/WEB_INF/jsp/hello.jsp");
>         //返货模型和视图对象
>         return modelAndView;
>     }
> }
> 
> ```
>
> `ModelAndView`对象封装了`模型数据`和`视图对象`，在使用视图解析器，把ModelAndView对象解析两个部分，一个是Mode和View，然后将mode渲染到View上面，返回给用户
>
> 在spring-config.xml配置后端控制器
>
> ```xml
> <!-- 配置后端控制器-->
> <bean name="/hello" class="com.wenqingwang.controller.HelloController"/>
> ```
>
> **jsp页面**
>
> ```jsp
> <%@ page contentType="text/html;charset=UTF-8"%>
> <html>
> <head>
>     <title>spring mvc</title>
> </head>
> <body>
> ${hello}
> </body>
> </html>
> ```

##### 配置Tomcat

> ![image.png](https://i.loli.net/2020/12/12/WZV8fIxmXlLz2iB.png)
>
> 在spring-config.xml配置视图解析器
>
> ```xml
>    <!--配置视图解析器-->
>     <!--InternalResourceViewResolver：支持jsp视图解析 -->
>     <!--viewClass：JstlView表示jsp模板需要使用jstl标签库，所以classpath中必须包含jstl的相关jar包-->
>     <!--
>     prefix和suffix：查找视图页面的后缀和前缀，最终视图地址为：前缀+逻辑视图名+后缀，逻辑视图名需要在Controlle中返回ModelAndView对象设置
>     -->
>     <!-- 最终的返回jsp地址是/WEB-INF/jsp/hello.jsp-->
>     <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
>         <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
>         <property name="prefix" value="/WEB-INF/jsp/"/>
>         <property name="suffix" value=".jsp"/>
>     </bean>
> 
> // modelAndView.setViewName("hello");控制器直接写hello==/WEB-INF/jsp/hello.jsp
> ```
>
> ------
>
> ​                                                                                         ==以上的是通过xml配置的spring  mvc==
>
> ------
>
> **配置日志文件**
>
> pom.xml
>
> ```xml
> <!--配置日志文件 log4j2-->
>         <dependency>
>             <groupId>org.apache.logging.log4j</groupId>
>             <artifactId>log4j-web</artifactId>
>             <version>2.13.1</version>
>         </dependency>
> ```
>
> **在src/main/resources创建log4j2.xml**
>
> ```xml
> <?xml version="1.0" encoding="UTF-8" ?>
> <Configuration  status="error">
>     <!--appenders:定义输出内容,输出格式,输出方式,日志保存策略等,常用其下三种标签[console,File,RollingFile]-->
>     <Appenders>
>         <Console name="Console" target="SYSTEM_OUT">
>             <PatternLayout pattern="[%d{HH:mm:ss:SSS}] [%p] - %l - %m%n"></PatternLayout>
>         </Console>
>     </Appenders>
>     <!--然后定义logger，只有定义了logger并引入的appender，appender才会生效-->
>     <!--优先级从高到低依次为：OFF、FATAL、ERROR、WARN、INFO、DEBUG、TRACE、 ALL。-->
>     <Loggers>
>         <Root level="INFO">
>             <AppenderRef ref="Console"></AppenderRef>
>         </Root>
>     </Loggers>
> </Configuration>
> ```
>
> 

#### spring mvc注解开发

##### pom.xml

> ```xml
>         <dependency>
>             <groupId>junit</groupId>
>             <artifactId>junit</artifactId>
>             <version>4.11</version>
>             <scope>test</scope>
>         </dependency>
>         <!--spring-webmvc 包含spring-aop，context，core，web，expression，beans-->
>         <dependency>
>             <groupId>org.springframework</groupId>
>             <artifactId>spring-webmvc</artifactId>
>             <version>${spring.version}</version>
>         </dependency>
> 
>         <!--java web begin-->
>         <dependency>
>             <groupId>javax.servlet</groupId>
>             <artifactId>javax.servlet-api</artifactId>
>             <version>4.0.1</version>
>         </dependency>
>         <dependency>
>             <groupId>javax.servlet</groupId>
>             <artifactId>jstl</artifactId>
>             <version>1.2</version>
>         </dependency>
>         <dependency>
>             <groupId>javax.servlet.jsp</groupId>
>             <artifactId>jsp-api</artifactId>
>             <version>2.0</version>
>         </dependency>
>         <!--java web end-->
>         <!--配置日志文件 log4j2-->
>         <dependency>
>             <groupId>org.apache.logging.log4j</groupId>
>             <artifactId>log4j-web</artifactId>
>             <version>2.13.1</version>
>         </dependency>
> 
> ```

##### 配置web.xml  和==上面一样==

> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
>          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>          xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
>          version="4.0">
>     <!--配置字符集编码过滤器-->
>     <filter>
>         <filter-name>characterEncodingFilter</filter-name>
>         <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
>         <init-param>
>             <param-name>encoding</param-name>
>             <param-value>UTF-8</param-value>
>         </init-param>
>         <init-param>
>             <param-name>forceEncoding</param-name>
>             <param-value>true</param-value>
>         </init-param>
>     </filter>
>     <filter-mapping>
>         <filter-name>characterEncodingFilter</filter-name>
>         <url-pattern>/*</url-pattern>
>     </filter-mapping>
>     <!--DispatcherServlet 配置前端控制器 servlet-->
>     <servlet>
>         <servlet-name>dispatcherServlet</servlet-name>
>         <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
>         <!--contextConfigLocation :指定spring mvc配置加载的位置
>    如果不指定则默认加载 WEB-INF/**-servlet.xml(例如：springmvc-serlet.xml)
>     -->
>         <init-param>
>             <param-name>contextConfigLocation</param-name>
>             <param-value>classpath:spring-config.xml</param-value>
>         </init-param>
>     </servlet>
>     <servlet-mapping>
>         <servlet-name>dispatcherServlet</servlet-name>
>         <!--可以拦截两种请求
>             第一种： 拦截固定后缀的URL，比如设置为*.do,*.action
>                     例如：/user/add.action 此方法比较简单，不会导致静态资源（jsp，js，css）被拦截
>             第二种：设置拦截所有 /
>                  例如：/user/add/ user/add.action此方法可以实现REST风格的url
>                       很多互联网类型应用使用这种方式
>                       但是此方法会导致静态资源（jsp，js，css）被拦截，需要特殊处理
>             错误设置：拦截所有，设置为/*
>         -->
>         <url-pattern>/</url-pattern>
>     </servlet-mapping>
> </web-app>
> ```

##### src/main/resources配置 spring-config.xml

> ```xml
>    <!--1.开启注解扫描-->
>     <context:component-scan base-package="com.wenqingwang.controller"/>
>     <!--2.注解处理器映射器
>       对类中标记@RequestMapping的方法进行映射
>       根据RequestMapping定义的url匹配
>       -->
> 
>     <bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping"/>
> 
>     <!--3.注解处理器适配器
>     对标记的RequestMapping的方法进行适配
>      -->
>     <bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter"/>
>     <!--4.后端处理器-->
>     <!--5.配置视图解析器-->
>     <!--InternalResourceViewResolver：支持jsp视图解析 -->
>     <!--viewClass：JstlView表示jsp模板需要使用jstl标签库，所以classpath中必须包含jstl的相关jar包-->
>     <!--
>     prefix和suffix：查找视图页面的后缀和前缀，最终视图地址为：前缀+逻辑视图名+后缀，逻辑视图名需要在Controlle中返回ModelAndView对象设置
>     -->
>     <!-- 最终的返回jsp地址是/WEB-INF/jsp/hello.jsp-->
>     <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
>         <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
>         <property name="prefix" value="/WEB-INF/jsp/"/>
>         <property name="suffix" value=".jsp"/>
>     </bean>
> ```

##### 注解驱动配置

> ```xml
> <!--spring mvc 使用 <mvc:annotation-driven/>
>         自动加载RequestMappingHandlerMapping和RequestMappingHandlerAdapter
>         可以使用 <mvc:annotation-driven/>替代注解映射器和注解适配器
>     -->
>     <mvc:annotation-driven/>
>     =========等于===============
>   <!--2.注解处理器映射器
>       对类中标记@RequestMapping的方法进行映射
>       根据RequestMapping定义的url匹配
>       -->
> 
>     <bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping"/>
> 
>     <!--3.注解处理器适配器
>     对标记的RequestMapping的方法进行适配
>      -->
>     <bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter"/>
> ```

##### 最终的src/main/resources配置 spring-config.xml

> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <beans xmlns="http://www.springframework.org/schema/beans"
>        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>        xmlns:context="http://www.springframework.org/schema/context"
>        xmlns:mvc="http://www.springframework.org/schema/mvc"
>        xsi:schemaLocation="http://www.springframework.org/schema/beans
>        http://www.springframework.org/schema/beans/spring-beans.xsd
>        http://www.springframework.org/schema/context
>        https://www.springframework.org/schema/context/spring-context.xsd
>        http://www.springframework.org/schema/mvc
>        https://www.springframework.org/schema/mvc/spring-mvc.xsd">
> 
>     <!--1.开启注解扫描-->
>     <context:component-scan base-package="com.wenqingwang.controller"/>
>     <!-- 2,3.spring mvc 使用 <mvc:annotation-driven/>
>         自动加载RequestMappingHandlerMapping和RequestMappingHandlerAdapter
>         可以使用 <mvc:annotation-driven/>替代注解映射器和注解适配器
>     -->
>     <mvc:annotation-driven/>
>     <!--4.后端处理器-->
>     <!--5.配置视图解析器-->
>     <!--InternalResourceViewResolver：支持jsp视图解析 -->
>     <!--viewClass：JstlView表示jsp模板需要使用jstl标签库，所以classpath中必须包含jstl的相关jar包-->
>     <!--
>     prefix和suffix：查找视图页面的后缀和前缀，最终视图地址为：前缀+逻辑视图名+后缀，逻辑视图名需要在Controlle中返回ModelAndView对象设置
>     -->
>     <!-- 最终的返回jsp地址是/WEB-INF/jsp/hello.jsp-->
>     <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
>         <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
>         <property name="prefix" value="/WEB-INF/jsp/"/>
>         <property name="suffix" value=".jsp"/>
>     </bean>
> </beans>
> ```

##### 控制器

> ```java
> @Controller
> public class HelloController {
>     //@RequestMapping 可以放在方法上或者类上 如果加载方法上，类上面写注解@RequestMapping可以不写参数
>     //value 请求的url value可以不写@RequestMapping("/hello")
>     //method 请求的类型 如：RequestMethod.GET RequestMethod.POST 如果不指定类型，可以请求全部
>     //@RequestParam 使用到参数前面 必须有的参数 如果参数可以为空required = false
>     @RequestMapping(value = "/hello",method = RequestMethod.GET)
>     public String hello(Model model,@RequestParam(value = "a",required = false) Integer a) {
>         System.out.println(a);
>         model.addAttribute("hello", "WenQingWang");
>         return "hello";
>     }
> 
> }
> ```

#### 注解

  