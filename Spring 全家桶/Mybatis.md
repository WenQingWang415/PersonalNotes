                                            Mybatis

### Mybatis简介

> Mybatis是一款优秀的持久框架，它支持自定义SQL，储存过程以及高级映射，Mybatis免除了几乎所有的JDBC代码以及设置参数和获取结果集的工作。Mybatis可以通过简单的XMl或注解来配置和映射原始类型，接口和java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

### Mybatis工作流程

>   ![工作流程](https://i.loli.net/2020/12/17/wVzOfvJlsnPSYB7.png)
>
> 1. 加载配置并初始化
>
>    加载配置文件。比如：全局配置文件，XXXmapeer.xml配置文件等
>
>    配置来源于两个地方：1.配置文件 2.java代码的注解，将SQL配置信息加载成为一个个MappedStatement对象（包括了传入参数映射配置，执行的SQL语句，结果映射配置），储存在内存中。
>
>    `MappedStatement维护了一条<select|update|delete|insert>节点的封装`
>
> 2. 接受调用请求
>
>    触发条件：调用mybatis提供的api
>
>    传入参数：为SQL的ID和传入参数的对象
>
>    处理过程：将请求传递给下层的请求处理层进行处理
>
> 3. 处理操作请求，触发条件：API接口层传递请求过来
>
>    传入参数：为SQL的ID和传入参数对象
>
>    具体处理流程：
>
>    1. 根据SQL的ID查找对应的`MappedStatement`对象
>    2. 根据传入参数对象解析`MappedStatement`对象，得到最终执行的SQL和执行传入参数
>    3. 获取数据库连接，根据得到的最终SQL语句和执行传入参数到数据库执行，并得到执行结果
>    4. 根据`MappedStatement`对象中的结果映射配置对得到的执行结果进行项目转换处理，并得到最终的处理结果
>    5. 释放连接资源
>
> 4. 返回处理结果
>
>    最终将处理结果返回
>
> **Mybatis大致流程：**
>
> ![image.png](https://i.loli.net/2020/12/17/MB31w8SAVEzuq7l.png)
>
> > **Mybatis配置**：
> >
> > -  全局配置文件：（配置数据源，事务运行等信息）
> > - 映射文件：（执行Statement的相关信息，包括SQL语句，输入参数，，输出结果）
> >
> > **SqlsessionFactory**（会话工厂），对连接池的封装，给连接池加了`thread local`锁，
> >
> > 作用：生产会话
> >
> > **SQLsession**（会话）对`Connection`的封装 。
> >
> > 作用：通过该接口可以对数据的进行增删查改
> >
> > **Execute**（执行器）支持缓存
> >
> > 作用：SQLsession本身不能直接操作数据库，需要通过execute接口来真正的操作数据库，该接口有两个实现：基本执行器，缓存执行器（默认）
> >
> > **Mapperstatement**集成了`statement`的接口，引入了对配置文件的功能，以及半orm的支持
> >
> > 作用：它封装执行`statement`的信息,包括SQL语句，输入参数，输出参数

### Mybatis整体架构

>   ![image.png](https://i.loli.net/2020/12/17/rcZ9IkTbVt4UBf6.png)
>
> 每一层的详解：
>
> ![image.png](https://i.loli.net/2020/12/17/jZGkNQ62XhzUbWY.png)

#### API接口层

> 核心对象`SqlSession` ,他是上层应用和Mybatis打交道的桥梁，Sqlsession中定义了非常多的数据库操作方法，在接口层调用请求时，会调用核心处理层的项目模块来完成对应的数据库操作

#### 数据处理层

> 这一层主要就是跟数据库的操作相关的都是在数据处理层完成的
>
> 核心处理层主要做四件事情：
>
> - 把接口中传入的参数解析并映射成JDBC类型
> - 解析xml文件中的sql语句，包括插入参数和动态语句生成
> - 执行SQL语句
> - 处理结果集，并映射成java对象
>
> 插件也属于核心层，这是由他的工作方式和拦截的对象决定的

#### 基础支撑层

> 负责最基础的功能支撑，包括连接管理，事务管理，配置加载和缓存处理，这些都是共用的东西，将他们抽取出来作为最基础的组件，为上层的数据处理层提供最基础的支撑
>
> ![image.png](https://i.loli.net/2020/12/17/P8fnHcNEsASiwtl.png)

### Mybatis主要的成员变量

#### Configuration

> Mybatis所有的配置信息都保存在configuration对象中，配置文件中的大部分配置都会储存到该类中

#### Sqlsession

> 作为Mybatis的工作的主要顶层API，表示和数据库交互会话，完成必要的增删查改功能

#### Executor

> Mybatis执行器，是Mybatis调度的核心，负责SQL语句的生成和查询缓存维护

#### StatementHandler

> 封装了JDBC Statement操作，负责JDBC Statement的操作，如设置参数等

#### ParamenterHandler

> 负责对用户传递参数转成JDBC Statement所对应的数据类型

#### ResultSetHandler

> 负责将JDBC返回Result结果集对象转成List类型的集合

#### TypeHandler

> 负责Java数据类型和JDBC数据类型之间的映射和转换

#### MappedStatement

> `MappedStatement`维护一条`<select|update|delete|insert>`节点的封装。

#### Sqlsouree

> 负责根据用户传递的paramenterObject，动态生成SQL语句，将信息封装到Boundsql对象中，并返回

#### Boundsql

> 表示动态生成的SQL语句以及相对应的参数信息

### Mybatis层次结构图

> ![image.png](https://i.loli.net/2020/12/17/asmEyMQk8wqBZxC.png)

### IntelliJ IDEA 统一设置编码为utf-8编码

> File->Settings->Editor->File Encodings
>
> ![image.png](https://i.loli.net/2020/12/09/dyW7oI42aekfwZt.png)

> idea安装lombok 注解生成get，set
>
> **安裝 Lombok**要在 project 中使用 lombok，除了要在 maven 中加入 lombok dependency，還要安裝 Intellij lombok 插件

**1. 加入maven dependency**

> ```xml
>        <dependency>
>             <groupId>org.projectlombok</groupId>
>             <artifactId>lombok</artifactId>
>             <version>1.18.16</version>
>             <scope>provided</scope>
>         </dependency>
> ```

**2. 在 Intellij 中安裝 lombok 插件**

> 先點選左上角 File->Settings->Plugins
>
> ![image.png](https://i.loli.net/2020/12/09/uY8PBDxMO5bzZtl.png)

### Mybatis入门案例

#### 创建一个maven项目

#### 添加pom.xml

> ```xml
>  <properties>
>         <!--        jdk1.8 -->
>         <java.version>1.8</java.version>
>         <!--        强制utf-8编码-->
>         <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
>     </properties>
> 
>     <dependencies>
>         <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
>         <dependency>
>             <groupId>org.projectlombok</groupId>
>             <artifactId>lombok</artifactId>
>             <version>1.18.16</version>
>             <scope>provided</scope>
>         </dependency>
> 
>         <!--mysql驱动-->
>         <dependency>
>             <groupId>mysql</groupId>
>             <artifactId>mysql-connector-java</artifactId>
>             <version>5.1.47</version>
>         </dependency>
>         <!--junit-->
>         <dependency>
>             <groupId>junit</groupId>
>             <artifactId>junit</artifactId>
>             <version>4.12</version>
>         </dependency>
>         <dependency>
>             <groupId>org.mybatis</groupId>
>             <artifactId>mybatis</artifactId>
>             <version>3.5.5</version>
>         </dependency>
>     </dependencies>
>     <build>
>         <resources>
>             <resource>
>                 <directory>src/main/resources</directory>
>                 <includes>
>                     <include>**/*.properties</include>
>                     <include>**/*.xml</include>
>                 </includes>
>                 <filtering>false</filtering>
>             </resource>
>             <resource>
>                 <directory>src/main/java</directory>
>                 <includes>
>                     <include>**/*.properties</include>
>                     <include>**/*.xml</include>
>                 </includes>
>                 <filtering>false</filtering>
>             </resource>
>         </resources>
>     </build>
> </project>
> ```

#### 配置全局配置文件

> mybatis-config.xml, 在图示位置( resources 目录)
>
> ```xml
> <?xml version="1.0" encoding="UTF-8" ?>
> <!DOCTYPE configuration
>         PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
>         "http://mybatis.org/dtd/mybatis-3-config.dtd">
> 
> <!--Mybatis全局配置文件-->
> <configuration>
>     <environments default="development">
>         <environment id="development">
>             <!--使用JDBC管理事务Mybatis-->
>             <transactionManager type="JDBC"/>
>             <!--数据库连接池，Mybatis内置的一个连接池-->
>             <dataSource type="POOLED">
>                 <property name="driver" value="com.mysql.jdbc.Driver"/>
>                 <property name="url" value="jdbc:mysql://118.31.45.168:3306/mybatis"/>
>                 <property name="username" value="root"/>
>                 <property name="password" value="root"/>
>             </dataSource>
>         </environment>
>     </environments>
> 
>     <!--每个*Mapper.xml都需要在这里注册-->
>     <mappers>
>         <mapper resource="com/mybatis/dao/UserMapper.xml"></mapper>
>     </mappers>
> </configuration>
> ```

#### 加载全局配置文件

> ```java
> package com.mybatis.util;
> import org.apache.ibatis.io.Resources;
> import org.apache.ibatis.session.SqlSession;
> import org.apache.ibatis.session.SqlSessionFactory;
> import org.apache.ibatis.session.SqlSessionFactoryBuilder;
> 
> import java.io.IOException;
> import java.io.InputStream;
> 
> // sqlSessionFactory --> sqlSession
> public class MybatisUtils {
>     private static SqlSessionFactory sqlSessionFactory;
>     static {
>         try {
>             String resource = "mybatis-config.xml";
>             InputStream inputStream = null;
>             //读取Mybatis全局配置文件
>             inputStream = Resources.getResourceAsStream(resource);
>             //	构建SQL会话工厂
>             sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
>         } catch (IOException e) {
>             e.printStackTrace();
>         }
>     }
> 
>     public static SqlSession getSqlSession(){
>         //从SQL会话工厂回去SQL会话
>         return sqlSessionFactory.openSession();
>     }
> }
> ```



#### 编写实体类

> ```java
> package com.mybatis.pojo;
> 
> import lombok.Data;
> 
> @Data
> public class User {
>     private int id;
>     private String name;
>     private String pwd;
> }
> 
> ```

#### 编写dao

> ```java
> package com.mybatis.dao;
> 
> import com.mybatis.pojo.User;
> 
> import java.util.List;
> 
> public interface UserDao {
>     List<User> getUserList();
> }
> ```

#### 编写Mapper文件

> Dao实现
>
> 不再写UserDaoImpl, 转而用哦一个Mapper配置文件
>
> UserMapper.xml in dao 包

> ```xml
> <?xml version="1.0" encoding="UTF-8" ?>
> <!DOCTYPE mapper
>         PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
>         "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
> <!--namespace命名空间 作用就是对SQL进行分类化管理，理解SQL隔离-->
> <mapper namespace="com.mybatis.dao.UserDao">
>     <!--select 查询语句-->
>     <!--
>      1. id属性：标识映射文件中的SQL，将SQL封装到 mapped statement对象中，所以称Statement的id
>      2. parameterType：指定输入参数类型
>      3.#{}：表示一个占位符
>      4.#{id}:其中的id表示接受的输入参数，如果输入参数是简单类型
>      5.#{}中的参数可以任意，可以为value或其他
>      6.resultType：指定SQL输出结果所映射的java对象类型
>         select指定的resultType表示将单条记录映射成java对象
> 
>     -->
>     <select id="getUserList" resultType="com.mybatis.pojo.User">
>         select * from user;
>     </select>
> </mapper>
> ```

#### 编写测试类

```java
import com.mybatis.dao.UserDao;
import com.mybatis.pojo.User;
import com.mybatis.util.MybatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.List;

public class UserDaoTest {
    @Test
    public void test(){
        /*获得SqlSession对象*/
        SqlSession sqlSession = MybatisUtils.getSqlSession();

        /*执行SQL
         *   方式一
         * */
        UserDao userDao = sqlSession.getMapper(UserDao.class);
        List<User> userList = userDao.getUserList();
        for (User user : userList) {
            System.out.println(user);
        }

        sqlSession.close();
    }
}
```

### Mapper代理开发方式

#### 开发规范

> - `mapper`接口的全限定名要和`mapper`映射文件的`namespace`值一致
>
>     ![image.png](https://i.loli.net/2020/12/17/5iGonESyZrJas2z.png)
>
> - `mapper`接口的方法名称要和`mapper`映射文件的`statement`的`id`一致
>
>     ![image.png](https://i.loli.net/2020/12/17/uOlNXCe3JgrTfH9.png)
>
> - `mapper`接口的方法参数类型要和`mapper`映射文件的`statement`的`paramenterType`的值一致
>
>     ![image.png](https://i.loli.net/2020/12/17/GxRmjNLI87aMCQ6.png)
>
> - `mapper`接口的方法返回值类型和`mapper`映射文件的`statement`的`resultType`的值一致
>
>     ![image.png](https://i.loli.net/2020/12/17/87IVkYxnluUpFcO.png)

### 日志配置

> [Log4j中文文档](https://www.docs4dev.com/docs/zh/log4j2/2.x/all/manual-configuration.html#AutomaticConfiguration)

#### 在pom.xml文件中引入log4j类库

> ```xml
> <dependency>
>     <groupId>org.apache.logging.log4j</groupId>
>     <artifactId>log4j-core</artifactId>
>     <version>2.11.2</version>
> </dependency>
> ```

#### 在resources目录下创建log4j2.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--status="WARN" :用于设置log4j2自身内部日志的信息输出级别，默认是OFF-->
<!--monitorInterval="30"  :间隔秒数,自动检测配置文件的变更和重新配置本身-->
<Configuration status="WARN" monitorInterval="30">
    <Appenders>
        <!-- 输出到控制台 -->
        <Console name="Console" target="SYSTEM_OUT">
            <!--<PatternLayout pattern="%d{HH:mm:ss.SSS}  [%t]  %-5level %logger{36} - %msg%n " />-->
            <!--添加有颜色字体
            IDEA中，点击右上角->Edit Configurations，在VM options中添加
            {在IDEA运行的旁边}
            -Dlog4j.skipJansi=false
            -->
            <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss.SSS} %highlight{%-5level} [%t] %highlight{%c{1.}.%M(%L)}: %msg%n"/>
            <!--
            格式化符号说明：
            %p：输出日志信息的优先级，即DEBUG，INFO，WARN，ERROR，FATAL。
            %d：输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，如：%d{yyyy/MM/dd HH:mm:ss,SSS}。
            %r：输出自应用程序启动到输出该log信息耗费的毫秒数。
            %t：输出产生该日志事件的线程名。
            %l：输出日志事件的发生位置，相当于%c.%M(%F:%L)的组合，包括类全名、方法、文件名以及在代码中的行数。例如：test.TestLog4j.main(TestLog4j.java:10)。
            %c：输出日志信息所属的类目，通常就是所在类的全名。
            %M：输出产生日志信息的方法名。
            %F：输出日志消息产生时所在的文件名称。
            %L:：输出代码中的行号。
            %m:：输出代码中指定的具体日志信息。
            %n：输出一个回车换行符，Windows平台为”rn”，Unix平台为”n”。
            %x：输出和当前线程相关联的NDC(嵌套诊断环境)，尤其用到像java servlets这样的多客户多线程的应用中。
            %%：输出一个”%”字符。

            另外，还可以在%与格式字符之间加上修饰符来控制其最小长度、最大长度、和文本的对齐方式。如：
            1) c：指定输出category的名称，最小的长度是20，如果category的名称长度小于20的话，默认的情况下右对齐。
            2)%-20c：”-“号表示左对齐。
            3)%.30c：指定输出category的名称，最大的长度是30，如果category的名称长度大于30的话，就会将左边多出的字符截掉，但小于30的话也不会补空格。
            -->
        </Console>
    </Appenders>
    <Loggers>
       <!--日志级别以及优先级排序: OFF > FATAL > ERROR > WARN > INFO > DEBUG > TRACE > ALL -->
        <Root level="DEBUG">
            <AppenderRef ref="Console"/>
        </Root>
    </Loggers>
</Configuration>
```

### 输入类型映射

#### 简单数据类型映射

> **一个参数**

> ```xml
> 
> <select id="getUsernane" resultType="com.mybatis.pojo.User" parameterType="java.lang.String">
>         <!--
>         模糊查询：
>        1. #{} 表示一个占位符号 相当于 jdbc中的 ? 符号
>             在控制器中添加百分号：“%测试%” 如：param.setUsername("%测试%"); 在 java 代码中传参的时候直接写上
>        2. ${value}中value值有限制只能写对应的value值不能随便写，
>          原样输出：'%测试%'
>          无法防止SQL注入，所以不推荐使用
>         3.CONCAT 拼接函数
>           AND name LIKE CONCAT(CONCAT('%',#{name},'%'))
>         4.bind标签
>          添加<bind name="name" value="'%'+neme+'%'"/>
>          where name like #{name}
>         -->
>         <bind name="name" value="'%'+neme+'%'"/>
>         select * from user
>         <!-- where name like #{name}-->
>         <!--where name like '%${value}%'-->
>         <!--where  name like CONCAT('%',#{naem},'%')-->
>         where name like #{name}
>     </select>
> ```

> **多个参数**
>
> 使用@Param注解
>
> ```java
>  /**
>      *如果多个参数
>      * 在参数前面使用@Param注解
>      */
> List<User> getUserNamePasswod(@Param("name") String name, @Param("pwd") String pwd);
> ```
>
> @Param("name")  CONCAT('%',#{name},'%') 这两个参数一致
>
> ```xml
>  <!--多个参数
>     -->
>     <select id="getUserNamePasswod" resultType="com.mybatis.pojo.User">
>         SELECT * FROM user where  
>         name like CONCAT('%',#{name},'%')  AND   pwd like CONCAT('%',#{pwd},'%')
>     </select>
> ```

#### 对象类型映射

> ```java
> //dao
> List<User> getUserNamePasswod1(User user);
> ```
>
> ```xml
>   <!--多个参数
>     -->
> <select id="getUserNamePasswod1" resultType="com.mybatis.pojo.User" 
>          parameterType="com.mybatis.pojo.User">
>         SELECT * FROM user 
>      where  name like CONCAT('%',#{name},'%') AND   pwd like CONCAT('%',#{pwd},'%')
>     </select>
> ```
>
> 测试：
>
> ```java
> @Test
>     public void test2(){
>         /*获得SqlSession对象*/
>         SqlSession sqlSession = MybatisUtils.getSqlSession();
> 
>         /*执行SQL
>          *   方式一
>          * */
>         UserDao userDao = sqlSession.getMapper(UserDao.class);
>         User user1=new User();
>         user1.setName("测试001");
>         user1.setPwd("123456");
>         List<User> userList = userDao.getUserNamePasswod1(user1);
>         for (User user : userList) {
>             System.out.println(user);
>         }
> 
>         sqlSession.close();
>     }
> ```
>
> 

#### Map集合类型映射

> ```java
> //dao
>  List<User> getUserNamePasswod2(Map<String, Object> map);
> ```
>
> ```xml
> <!--#{name}要和map中的Key一致-->
>     <select id="getUserNamePasswod2" resultType="com.mybatis.pojo.User" 
>             parameterType="java.util.Map">
>         SELECT * FROM user 
>         where  name like CONCAT('%',#{name},'%') AND   pwd like CONCAT('%',#{pwd},'%')
>     </select>
> ```
>
> 测试：
>
> ```java
> @Test
>     public void test3(){
>         /*获得SqlSession对象*/
>         SqlSession sqlSession = MybatisUtils.getSqlSession();
> 
>         /*执行SQL
>          *   方式一
>          * */
>         UserDao userDao = sqlSession.getMapper(UserDao.class);
>         Map<String, Object> map =new HashMap();
>         map.put("name","测试001");
>         map.put("pwd","123456");
>         List<User> userList = userDao.getUserNamePasswod2(map);
>         for (User user : userList) {
>             System.out.println(user);
>         }
> 
>         sqlSession.close();
>     }
> ```

#### 主键回写

> ```java
> //dao
> void  adduser(User user);
> ```
>
> ```xml
> <!--第一种：主键回写
>             keyProperty:指定对象的那个属性是主键
>             keyColumn：指定数据库主键列的名称
>             useGeneratedKeys：参数只对insert有效。默认是false
>                        当设置为ture时，表示如果插入的表以自增为主键，则允许JDBc支持自动生成，并将自动生成的主键返回
>     -->
>     <insert id="adduser" parameterType="com.mybatis.pojo.User"
>             keyProperty="id" keyColumn="id" useGeneratedKeys="true">
>         INSERT into
>         user(name,pwd)
>         value (#{name},#{pwd})
>     </insert>
> <!--第二种：主键回写LAST_INSERT_ID
>         keyProperty:指定对象的那个属性主键
>         keyColumn：指定数据库主键列的名称
>         resultType：主键java的类型
>         order：
>              AFTER：在insert语句执行之后再去获取主键的值，如：数据库主键自动增长是使用
>              BEFORE：在update语句执行前再去获取主键的值，如：数据库主键UUID
> -->
>     <insert id="adduser" parameterType="com.mybatis.pojo.User">
>         <selectKey keyProperty="id" keyColumn="id" resultType="java.lang.Integer" order="AFTER">
>             select LAST_INSERT_ID()
>         </selectKey>
>         INSERT into
>         user(name,pwd)
>         value (#{name},#{pwd})
>     </insert>
> <!--第三种：主键回写UUID
>         keyProperty:指定对象的那个属性主键
>         keyColumn：指定数据库主键列的名称
>         resultType：主键java的类型
>         order：
>              AFTER：在insert语句执行之后再去获取主键的值，如：数据库主键自动增长是使用
>              BEFORE：在update语句执行前再去获取主键的值，如：数据库主键UUID
>        数据库的ID是String类型的，
> -->
>     <insert id="adduserUUID" parameterType="com.mybatis.pojo.UserUUID">
>         <selectKey keyProperty="id"  resultType="java.lang.String" order="BEFORE">
>             select UUID()
>         </selectKey>
>         INSERT into
>         user(id,name,pwd)
>         value (#{id},#{name},#{pwd})
>     </insert>
> ```
>
> 测试：
>
> ```java
> @Test
>     public void test4(){
>         /*获得SqlSession对象*/
>         SqlSession sqlSession = MybatisUtils.getSqlSession();
> 
>         /*执行SQL
>          *   方式一
>          * */
>         UserDao userDao = sqlSession.getMapper(UserDao.class);
>         User user1=new User();
>         user1.setName("测试001");
>         user1.setPwd("123456");
>         userDao.adduser(user1);
>         sqlSession.commit();
>         System.out.println(user1.getId());
> 
>         sqlSession.close();
>     }
> ```

### 输出类型映射

#### resultType

> 使用要求
>
> - 使用resultType进行结果映射时，需要查询出的列名和映射的对象属性名一致，才能映射成功
> - 如果查询的列名和对象的属性名全部不一致，那么映射为空
> - 如果查询的列名和对象的属性名有一个一致，那么映射的对象不为空，但是映射正确的才会有值
> - 如果查询的SQL列名有别名，那么这个别名就是属性映射的列名

**输出基本类型**

> 注意：对简单类型的结果映射也是有要求的，查询的必须是一列，才能映射简单类型

**输出对象或者集合**

> - 返回List
>
>   ```java
>   List<User> getUserList();
>   ```

#### resultMap

> ```xml
>   <!--完成数据库列名和对象名称之间的映射关系-->
>     <resultMap id="UserMap" type="com.mybatis.pojo.User">
>         <!--主键-->
>         <id property="id" column="id"/>
>         <!--普通列-->
>         <result property="name" column="name"/>
>     </resultMap>
>  <!--使用resultMap=“id”-->
>     <select id="getUserList" resultMap="UserMap">
>         select * from user
>     </select>
> ```

### 动态SQL

> 在Mybatis中，它提供了一些动态SQL标签，可以更快速开发

常用的SQL动态标签

> - if标签
> - where标签
> - SQL片段
> - foreach标签

#### where和if标签

> ```xml
> 
>     <select id="getUserNamePasswod1" resultMap="UserMap">
>         SELECT * FROM user
>         <!--where标签可以去掉查询条件中的第一个and关键字-->
>         <where>
>         <if test="name !=null and name!=''">
>             AND  name like CONCAT('%',#{name},'%')
>         </if>
>             <if test="pwd !=null and pwd!=''">
>                 AND   pwd like CONCAT('%',#{pwd},'%')
>             </if>
> 
>         </where>
> 
>     </select>
> ```

#### SQL片段

> ```xml
> <select id="getUserNamePasswod1" resultMap="UserMap">
>         SELECT * FROM user
>        <!--引入SQL片段-->
>         <include refid="wheresql"/>
>     </select>
>     <!-- sql片段-->
>     <sql id="wheresql">
>         <!--where标签可以去掉查询条件中的第一个and关键字-->
>         <where>
>             <if test="name !=null and name!=''">
>                 AND name like CONCAT('%',#{name},'%')
>             </if>
>             <if test="pwd !=null and pwd!=''">
>                 AND pwd like CONCAT('%',#{pwd},'%')
>             </if>
> 
>         </where>
> 
>     </sql>
> ```

#### foreach标签

> ```java
> //dao
>  /**
>      * 通过id查询集合
>      * @param ids
>      * @return
>      */
>    List<UserUUID> getbyid(@Param("ids") List<Integer> ids);
> ```
>
> ```xml
>     <!-- 第一种使用in（6,7,9）
> -->
> <select id="getbyid" resultMap="UserMap" parameterType="java.util.List">
>         <!--
>         使用foreach遍历传入ids
>             collection:指定输入对象中的集合名称
>             item:每次生成遍历的对象
>             open:开始遍历时拼接的字符串
>             close：解释遍历时拼接字符串
>             separator:分割符：遍历两个对象中需要拼接的串
>         -->
>         select  * from user
>         <where>
>             <foreach collection="ids" item="item_id" open="and id in (" separator="," close=")">
>                 #{item_id}
>             </foreach>
>         </where>
>     </select>
> <!-- 第二种使用or拼接
> -->
>   <select id="getbyid" resultMap="UserMap" parameterType="java.util.List">
>         <!--
>         使用foreach遍历传入ids
>             collection:指定输入对象中的集合名称
>             item:每次生成遍历的对象
>             open:开始遍历时拼接的字符串
>             close：解释遍历时拼接字符串
>             separator:分割符：遍历两个对象中需要拼接的串
>         -->
>         select  * from user
>         <where>
>             <foreach collection="ids" item="item_id" open="and  " separator="or" close="">
>              id=   #{item_id}
>             </foreach>
>         </where>
>     </select>
> ```
>
> 测试
>
> ```java
>  @Test
>     public void test6(){
>         /*获得SqlSession对象*/
>         SqlSession sqlSession = MybatisUtils.getSqlSession();
> 
>         /*执行SQL
>          *   方式一
>          * */
>         UserDao userDao = sqlSession.getMapper(UserDao.class);
>        List<Integer> ids = new ArrayList();
>        ids.add(6);
>        ids.add(7);
>        ids.add(9);
>         List<UserUUID> userList = userDao.getbyid(ids);
>         for (UserUUID user : userList) {
>             System.out.println(user);
>         }
> 
>         sqlSession.close();
>     }
> ```

### 高级映射

> 

