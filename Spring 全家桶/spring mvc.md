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

开发Controller需要实现`import org.springframework.web.servlet.mvc.Controller`

```java

public class HelloController implements Controller {

 @Override
 public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {

     ModelAndView modelAndView = new ModelAndView();
     //设置数据到模型
     modelAndView.addObject("hello","spring mvc");
     //设置逻辑视图路径
     modelAndView.setViewName("/WEB_INF/jsp/hello.jsp");
     //返货模型和视图对象
     return modelAndView;
 }
}

```

`ModelAndView`对象封装了`模型数据`和`视图对象`，在使用视图解析器，把ModelAndView对象解析两个部分，一个是Mode和View，然后将mode渲染到View上面，返回给用户

在spring-config.xml配置后端控制器

```xml
<!-- 配置后端控制器-->
<bean name="/hello" class="com.wenqingwang.controller.HelloController"/>
```

**jsp页面**

```jsp
<%@ page contentType="text/html;charset=UTF-8"%>
<%@taglib uri="http://java.sun.com/jstl/fmt" prefix="fmt"%>
<%@ taglib prefix="C" uri="http://java.sun.com/jsp/jstl/core" %>
<%--获取上下文路径--%>
<C:set var="ctx" value="${pageContext.request.contextPath}"/>
<%--使用方式
    加载静态资源前面和请求前面
     <link href="${ctx}/hello.jsp">
    --%>

<html>
<head>
 <title>spring mvc</title>
</head>
<body>
${hello}
</body>
</html>
```

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
>     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>     xmlns:context="http://www.springframework.org/schema/context"
>     xmlns:mvc="http://www.springframework.org/schema/mvc"
>     xsi:schemaLocation="http://www.springframework.org/schema/beans
>     http://www.springframework.org/schema/beans/spring-beans.xsd
>     http://www.springframework.org/schema/context
>     https://www.springframework.org/schema/context/spring-context.xsd
>     http://www.springframework.org/schema/mvc
>     https://www.springframework.org/schema/mvc/spring-mvc.xsd">
> 
>  <!--1.开启注解扫描-->
>  <context:component-scan base-package="com.wenqingwang.controller"/>
>  <!-- 2,3.spring mvc 使用 <mvc:annotation-driven/>
>      自动加载RequestMappingHandlerMapping和RequestMappingHandlerAdapter
>      可以使用 <mvc:annotation-driven/>替代注解映射器和注解适配器
>  -->
> <mvc:annotation-driven/>
> <!--不拦截静态资源-->
> <mvc:default-servlet-handler/>
>  <!--4.后端处理器-->
>  <!--5.配置视图解析器-->
>  <!--InternalResourceViewResolver：支持jsp视图解析 -->
>  <!--viewClass：JstlView表示jsp模板需要使用jstl标签库，所以classpath中必须包含jstl的相关jar包-->
>  <!--
>  prefix和suffix：查找视图页面的后缀和前缀，最终视图地址为：前缀+逻辑视图名+后缀，逻辑视图名需要在Controlle中返回ModelAndView对象设置
>  -->
>  <!-- 最终的返回jsp地址是/WEB-INF/jsp/hello.jsp-->
>  <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
>      <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
>      <property name="prefix" value="/WEB-INF/jsp/"/>
>      <property name="suffix" value=".jsp"/>
>  </bean>
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

#### json需要的pom.xml

```xml
 <!--引入json的依赖-->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>2.11.2</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.11.2</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-annotations</artifactId>
            <version>2.11.2</version>
        </dependency>
```



#### 注解

##### @RequestMapping

```java
/**
 *@RequestMapping
 * 属性：
 *    1）value：请求的url
 *    2）method：设置HTTP方法 如：get请求 method = RequestMethod.GET
 *    3）spring 4.3开始可用 @GetMapping @PostMapping  @PutMapping @DeleteMapping @PatchMapping 是@RequestMapping的不同变体
 *       其HTTP方法分别使用 GET，POST，PUT,DELETE,PATCH  
 *    */
```

#####   @DateTimeFormat

> ```java
>  /**
>      * 一般使用在页面传到控制器日期格式化
>      * @DateTimeFormat  声明字段或方法参数应格式化为日期或时间。
>      * pattern：用于格式化字段的自定义模式。
>      */
>     @DateTimeFormat(pattern = "yyyy-MM-dd")
>     private  Date datime;
> ```

##### @ResponseBody

> ```java
> 该@ResponseBody注解告诉控制器返回的对象将自动序列化为JSON，并通过回的HttpResponse对象。 返回json数据
> 
> 假设我们有一个自定义的Response对象：
> 
> public class ResponseTransfer {
>     private String text; 
>     
>     // standard getters/setters
> }
> 接下来，可以实现关联的控制器：
> 
> @Controller
> @RequestMapping("/post")
> public class ExamplePostController {
> 
>     @Autowired
>     ExampleService exampleService;
> 
>     @PostMapping("/response")
>     @ResponseBody
>     public ResponseTransfer postResponseController(
>       @RequestBody LoginForm loginForm) {
>         return new ResponseTransfer("Thanks For Posting!!!");
>      }
> }
> 在浏览器的开发者控制台或使用Postman之类的工具，我们可以看到以下响应：
> 
> {"text":"Thanks For Posting!!!"}
> 记住，我们不需要用@ResponseBody注释对@RestController注释的控制器进行注释，因为默认情况下Spring会这样做。
> ```

##### @RequestBody

```xml
/**
 * RequestBody 接受json数据
 * 该@RequestBody注解的映射的HttpRequest对象，自动反序列化到java对象
 *
 */
@PostMapping("/request")
public ResponseEntity postController(
        @RequestBody LoginForm loginForm) {

    exampleService.fakeAuthenticate(loginForm);
    return ResponseEntity.ok(HttpStatus.OK);
}
/**
* @RequestBody 默认从客户端发送相对应的json数据
*/
public class LoginForm {
    private String username;
    private String password;
    // ...
}
//HttpRequest主体的对象映射到我们的LoginForm对象。 必须和pojo值对应
/**
 * 格式：{"username": "johnny", "password": "password"}
 */

```



##### @PathVariable

> ```java
> //统一请求链接：http://localhost:8080/hello1/1   /直接拼接参数
> /**
>      * 第一种简单的映射
>      * 该@PathVariable注释可以被用于处理在请求URI映射模板变量
>      */
>     @RequestMapping("/hello1/{id}")
>     @ResponseBody
>     public String zhujie1(@PathVariable Integer id) {
>         return "id"+id;
>     }
> 
>     /**
>      * 第一种：如果路径变量名不同，我们可以指定
>      * 该@PathVariable注释可以被用于处理在请求URI映射模板变量
>      */
>     @RequestMapping("/hello2/{id}")
>     @ResponseBody
>     public String zhujie2(@PathVariable("id") Integer employeeId) {
>         return "id"+employeeId;
>     }
> 
>     /**
>      * 第三种：请求中有多个变量
>      * 该@PathVariable注释可以被用于处理在请求URI映射模板变量
>      */
>     @RequestMapping("/hello3/{id}/{name}")
>     @ResponseBody
>     public String zhujie3(@PathVariable Integer id, @PathVariable String name) {
>         return "id"+id+"name"+name;
>     }
> 
>     /**
>      * 第四种：使用类型为java.util.Map <String，String>的方法参数来处理多个@PathVariable参数：
>      * 该@PathVariable注释可以被用于处理在请求URI映射模板变量
>      */
>     @RequestMapping("/hello4/{id}/{name}")
>     @ResponseBody
>     public String zhujie4(@PathVariable Map<String, String> pathmap) {
>         String id = pathmap.get("id");
>         String name = pathmap.get("name");
>         if (id != null && name != null) {
>             return "ID: " + id + ", name: " + name;
>         } else {
>             return"Missing Parameters";
>         }
> 
>     }
> 
>     /**
>      * 第五种：可选路径变量，由于默认情况下@PathVariables注释的方法参数是必需的
>      * 该@PathVariable注释可以被用于处理在请求URI映射模板变量
>      *@PathVariable的required属性设置为false，以使其可选 设置false可以传参数可以不传参数都不会报错
>      */
>     @RequestMapping(value = {"/hello5","/hello5/{id}"})
>     @ResponseBody
>     public String zhujie5(@PathVariable(required = false) Integer id) {
> 
>       return "id"+id;
> 
>     }
> ```

##### @JsonFormat

> ```java
> /**
>  * 需要引入json的包 json需要的pom.xml
>  * 在pojo中使用，在属性上面定义
>  * pattern：表示时间格式
>  * timezone：是时间设置为东八区，避免时间在转换中有误差
>  */
> @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss",timezone="GMT+8")
> private  Date date1;
> ```

####  文件上传

##### 引入pom.xml

```xml
<!--文件上传-->
        <dependency>
            <groupId>commons-fileupload</groupId>
            <artifactId>commons-fileupload</artifactId>
            <version>1.4</version>
        </dependency>
```

##### spring-config.xml配置文件解析器

```xml
    <!--文件上传解析器-->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <!--限制文件的大小，不设置没有默认，单位为字节200*1024**1204 =200M-->
        <property name="maxUploadSize" value="209715200"/>
        <!--设置每个上传文件的大小上线 1024*1024*2=200M-->
        <property name="maxUploadSizePerFile" value="209715200"/>
        <!--处理文件乱码-->
        <property name="defaultEncoding" value="UTF-8"/>
        <!--resolveLazily属性启动是为了推迟文件解析 以便获取文件大小异常-->
        <property name="resolveLazily" value="true"/>
    </bean>s
```

#### 拦截器

##### 定义拦截器

```java
package com.wenqingwang.interceptor;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class AuthInterceptor  implements HandlerInterceptor {
    /**
     * 在后端控制器方法调用前执行
     * 返回值是否中断
     * true 表示继续执行（下一个拦截器或处理器）
     * false则会中断后续的所有操作，所以需要使用response来继续响应后续的请求
     */
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        return false;
    }

    /**
     *在后端控制器方法调用后，解析视图前调用，可以对视图和模型做进一步修改和渲染
     * 可在ModelAndView中加入数据，比如时间
     */
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {

    }

    /**
     *整个请求完成，即视图渲染结束后调用，可以清理资源，比如日志
     */
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }
}

```

##### spring-config.xml配置拦截器

```xml
<!--配置拦截器-->
    <mvc:interceptors>
        <!--匹配是url路径 如果不配置/**,将拦截所有的controller-->
        <mvc:interceptor>
            <!--拦截所有-->
            <mvc:mapping path="/**"/>
            <mvc:exclude-mapping path="/login"/>
            <mvc:exclude-mapping path="/css/**"/>
            <mvc:exclude-mapping path="/js/**"/>
            <mvc:exclude-mapping path="/fonts/**"/>
            <mvc:exclude-mapping path="plugin/**"/>
            <bean class="com.wenqingwang.interceptor.AuthInterceptor"/>
        </mvc:interceptor>
    </mvc:interceptors>
```

