##                                                                      Maven

### Maven介绍

> Maven是跨平台的项目管理工具
>
> ​     作用：主要服务于java平台，项目构建，依赖管理
>
> Maven是基于POM( Project Object Model，项目对象模型 ) 

### MaVen的安装

#### 第一步：安装jdk 

>    要求：
>
> ​          Maven 3.0 / 3.1要求JDK 1.5或以上
>
> ​          Maven 3.2要求JDK 1.6或以上
>
> ​          Maven 3.3要求JDK 1.7或以上

#### 第二步:安装Maven

> [Maven](https://maven.apache.org/download.cgi)下载
>
> ![image.png](https://i.loli.net/2020/12/15/gKdLTjPBwh9irSb.png)
>
> Maven目录说明：
>
> ![image.png](https://i.loli.net/2020/12/15/XwROhL6W3UvA95s.png)

#### 第三步：配置Maven环境变量

> 首先配置 系统变量 MAVEN_HOME ==变量名称固定不能改==
>
> ![image.png](https://i.loli.net/2020/12/15/WamZRD6qixEks1J.png)
>
> 然后配置环境变量：%MAVEN_HOME%\bin
>
> ![image.png](https://i.loli.net/2020/12/15/4DLZWVREmTKOdcS.png)
>
> ==**然后一路确定**，**保存环境变量**==
>
> 校验是否配置成功
>
> 在cmd命令输入`mvn -v`输出信息如图：
>
> ![image.png](https://i.loli.net/2020/12/15/PfTASErNxUK2mjV.png)
>
> 

#### 第四步：本地仓库配置

> 本地仓库默认位置在：`当前用户名\.m2\repository` 可以自定义但是不建议
>
> 1. 默认位置隐蔽，不易查找
> 2. 本地的jar可以放在默认位置，内存问题
>
> 配置自定义的本地仓库位置`conf/settings.xml`中配置自定义仓库
>
> ![image.png](https://i.loli.net/2020/12/15/svoUXnY5yrIZh7x.png)
>
> 

#### 第五步：远程镜像配置

> [阿里云镜像文档](https://help.aliyun.com/document_detail/102512.html?spm=a2c40.aliyun_maven_repo.0.0.36183054eGk3vS)
>
> 打开maven的配置文件(windows机器一般在maven安装目录的conf/settings.xml)，在`<mirrors></mirrors>`标签中添加mirror子节点:
>
> ```xml
> <mirror>
>     <id>aliyunmaven</id>
>     <mirrorOf>*</mirrorOf>
>     <name>阿里云公共仓库</name>
>     <url>https://maven.aliyun.com/repository/public</url>
> </mirror>
> ```
>
> ![image.png](https://i.loli.net/2020/12/15/eMRNY3UIAtsEfvB.png)

### idea中配置Maven

> ![image.png](https://i.loli.net/2020/12/15/NQVA14IXw3t6UuM.png)

### Maven常用的命令

> 需要在pom.xml所在目录下执行的命令

#### mvn compile

> 执行 mvn compile 完成编译工作
>
> 执行完毕之后，会生成target目录。该目录存放了编译后的字节码文佳

#### mvn clean

> 执行 mvn cleanmingl
>
> 执行完毕后会删除 target目录

#### mvn test

> 执行 mvn test执行单元测试操作
>
> 执行完毕后 会在target目录中生成三个文件夹，surefire,surefire-reports（测试报告），test-class（测试字节码文件）

#### mvn package

> 执行 mvn package命令，完成打包工作
>
> 执行命令完成后，会在target目录中生成一个文件，该文件可能是jar，war

#### mvn install

> 执行mvn install 完成打好的jar包安装到本地仓库
>
> 执行完毕后，会在本地仓库出现安装的jar包，方便其他工程应用

#### mvn clea compile

>  cmd 录入mvn clean compile命令
>
> 组合指令，先执行 clean 在执行compile 通常应用于上线前执行，清除测试类

#### mvn clean test

> cmd 录入mvn clean test命令
>
> 组合指令，先执行clean 在执行test 通常应用于测试环节

#### mvn clean package

> cmd录入 mvn clean package命令
>
> 组合指令 先执行clean 在执行package。将项目打包，通常应用于发布前
>
> 执行过程：
>
>  清理--------清空环境
>
> 编译---------编译源码
>
> 测试---------测试源码
>
> 打包-------将编译的非测试类打包

#### mvn clean install 

> cmd 录入 mvn clean install
>
> 组合指令 先执行clean 在执行 install ，将项目打包，通常应用于发布前

### idea执行命令

> ![image.png](https://i.loli.net/2020/12/15/JTEV7Zb9jIvxHri.png)

### Maven核心概念

#### Maven坐标

> ```xml
> <dependencies>
>   <dependency>
>     <groupId>junit</groupId>
>     <artifactId>junit</artifactId>
>     <version>4.11</version>
>     <scope>test</scope>
>   </dependency>
> </dependencies>
> ```
>
> dependencies ：    在dependencies  标签中添加项目需要的jar所对应的maven坐标
>
> dependency：    一个dependency 表示一个坐标
>
> groupId：     定义当前Maven组织名称
>
> artifactId：    定义实际项目名称
>
> version：     定义当前项目的当前版本号
>
> scope  依赖范围
>
> | 依赖范围 |                  编译有效                   |                  测试有效                   |                 运行时有效                  |                  打包有效                   |       例子        |
> | :------: | :-----------------------------------------: | :-----------------------------------------: | :-----------------------------------------: | :-----------------------------------------: | :---------------: |
> | compile  | <span style="color:cornflowerblue">✔</span> | <span style="color:cornflowerblue">✔</span> | <span style="color:cornflowerblue">✔</span> | <span style="color:cornflowerblue">✔</span> |    spring-core    |
> |   test   |      <span style="color:red">✘</span>       | <span style="color:cornflowerblue">✔</span> |      <span style="color:red">✘</span>       |      <span style="color:red">✘</span>       |       junit       |
> | provided | <span style="color:cornflowerblue">✔</span> | <span style="color:cornflowerblue">✔</span> |      <span style="color:red">✘</span>       |      <span style="color:red">✘</span>       |    servlet-api    |
> | runtime  |      <span style="color:red">✘</span>       | <span style="color:cornflowerblue">✔</span> | <span style="color:cornflowerblue">✔</span> | <span style="color:cornflowerblue">✔</span> |     JDBC驱动      |
> |  system  | <span style="color:cornflowerblue">✔</span> | <span style="color:cornflowerblue">✔</span> |      <span style="color:red">✘</span>       |      <span style="color:red">✘</span>       | 本地maven之外的库 |

#### Maven依赖传递

> A->B(compile)   第一关系: a依赖b  compile
>
> B->C(compile)   第二关系: b依赖c  compile
>
> ```xml
> 当在A中配置
> <dependency>  
>             <groupId>com.B</groupId>  
>             <artifactId>B</artifactId>  
>             <version>1.0</version>  
> </dependency>
> ```
>
> ![image.png](https://i.loli.net/2020/12/16/vVf4HtqnPBLARke.png)

#### 依赖冲突

> 如果直接依赖和间接依赖中包含有同一个坐标不同版本的资源依赖 ，以直接依赖的版本为准（就近原则）
>
> ![image.png](https://i.loli.net/2020/12/16/lgUKGEYhvDw4BV2.png)
>
> 
>
> 如果直接依赖中包含同一个坐标不同版本的资源依赖，以配置顺序下方的版本为准（就近原则）
>
> ![image.png](https://i.loli.net/2020/12/16/vVmGYE835pN4Akc.png)
>
> 



#### 可选依赖

> ```xml
> <optional>true/false</optional>
> ```
>
> 是否可选，理解为是否向下传递
>
> 在依赖中添加`optional`选项决定依赖是否向下传递，如果是true向下传递，如果是false不向下传递，默认是false
>
> ```xml
>  <dependency>
>         <groupId>junit</groupId>
>         <artifactId>junit</artifactId>
>         <version>3.8.2</version>
>         <scope>test</scope>
>         <optional>false</optional>
>     </dependency>
> ```
>
> 

#### 排除依赖（==<span style="background:red">可以解决包冲突</span>==）

> 排除依赖包中所包含的关系，不需要添加版本号
>
> 如果在本次依赖有多余的jar包被传递依赖过来，如果想把这些表排除的话可以配置exclusions进行排除
>
> ```xml
>  <!--spring-webmvc 包含spring-aop，context，core，web，expression，beans-->
>         <dependency>
>             <groupId>org.springframework</groupId>
>             <artifactId>spring-webmvc</artifactId>
>             <version>5.2.6.RELEASE</version>
>             <!--排除依赖-->
>             <exclusions>
>                 <exclusion>
>                     <groupId>org.springframework</groupId>
>                     <artifactId>spring-aop</artifactId>
>                 </exclusion>
>             </exclusions>
>         </dependency>
> ```
>
> ![image.png](https://i.loli.net/2020/12/16/tkc4fxFDEI6BKJv.png)

### 生命周期

#### 什么是生命周期？

> Maven生命周期就是为了对**所有的构建过程进行抽象和统一**，包括项目的清理，初始化，编译，打包，测试，部署等几乎所有构建的步骤

#### 生命周期构建工程的步骤

在Maven中有<span style="color:red">“三套”“相互独立”</span>的生命周期，这三套生命周期分别是：

> `Clean Lifecycle`:在真正构建之前进行一些清理工作
>
> `Default Lifecycle`:构建核心部分，**编译，测试，打包，部署等等**
>
> `Site Lifecycle`:生成项目报告，站点，发布站点

> 他们是相互独立的，你可以仅仅调用`clean`清理或者调用`site`生成站点，也可以直接运行 `mvn clean install site`运行所有这三套的生命周期

#### Maven三大生命周期

##### clean生命周期

> 当我们调用 mvc post-clean命令是，Maven调用生命周期，包含几个阶段：
>
> - pre-clean：执行一些需要在clean之前完成的工作
> - clean：移除所有上一次构成生成的文件
> - post-clean：执行一些在需要clean之后立刻完成的工作
>
> 如果执行 `mvn clean`将会运行以下两个生命周期阶段：
>
> ```cmd
> pre-clean ,clean
> ```
>
> 如果执行 `mvn post-clean`将会运行以下三个生命周期阶段：
>
> ```mnd
> pre-clean, clean ,post-clean
> ```

##### default（BUlid）生命周期

> 这是maven的主要生命周期，包括下面23个阶段
>
> |                生命周期阶段                |                            描述                            |
> | :----------------------------------------: | :--------------------------------------------------------: |
> |              validate（校验）              |    校验项目是否正确并且所有必要的信息可以完成项目的构建    |
> |            initialize（初始化）            |               初始化构建状态，比如设置属性值               |
> |       generate-sources（生成源代码）       |                生成包含编译阶段中的任何代码                |
> |       process-sources（处理源代码）        |                处理源代码，比如：过滤任意值                |
> |     genrate-resources（生成资源文件）      |              生成将会包含在项目包中的资源文件              |
> |     process-resources（处理资源文件）      |         复制和处理资源到目标目录，为打包阶段做准备         |
> |              compile（编译）               |                      编译项目的源代码                      |
> |       process-classes（处理类文件）        |  处理编译生成的文件，比如对java class文件做字节码改善优化  |
> |   genrate-test-sources（生成测试源代码）   |                生成包含编译阶段的任何源代码                |
> |   process-test-sources（处理测试源代码）   |                       处理测试源代码                       |
> | genrate-test-resources（生成测试资源文件） |                     为测试创建资源文件                     |
> | process-testresources（处理测试资源文件）  |                复制和处理测试资源到目标目录                |
> |       test-compile（编译测试源代码）       |                  编译测试源代码到测试目录                  |
> |    process-test-classes（处理测试文件）    |                处理测试源代码编译生成的文件                |
> |                test（测试）                |        使用单元测试框架运行测试 如：juint是其中之一        |
> |        prepare-package（准备打包）         |         在是实际打包之前，执行任何有必要的打包准备         |
> |               package(打包)                | 将编译好的文件打包可分发格式的文件，比如jar，war，ear文件  |
> |     pre-integration-test（集成测试前）     |      在执行集成测试环境进行必要的动作，比如：环境搭建      |
> |        integration-test（集成测试）        |              处理和部署到可运行集成测试环境中              |
> |       post-integration（集成测试后）       | 在执行集成测试完成后进行必要的动作，比如：清理集成测试环境 |
> |               verify（验证）               |         运行任意的检查来验证项目包有效达到质量标准         |
> |              install（安装）               |   安装项目包到本地仓库，这样项目包可以用作其他项目的依赖   |
> |               deploy（部署）               |        最终的项目包复制到远程仓库中与其他开发者共享        |
>
> 有一些与 Maven 生命周期相关的重要概念需要说明：
>
> 当一个阶段通过 Maven 命令调用时，例如 mvn compile，只有该阶段之前以及包括该阶段在内的所有阶段会被执行。
>
> 不同的 maven 目标将根据打包的类型（JAR / WAR / EAR），被绑定到不同的 Maven 生命周期阶段。

##### site 生命周期

> Maven Site插件一般用来创建新的报告，文档，部署站点等
>
> - pre-site：执行一些需要在生成站点文档完成的工作
> - site：生成项目站点文档
> - post-site：执行一些需要生成站点文档之后完成的工作，并且为部署做准备
> - site-deploy：将生成的站点文档部署到特定的服务器上

### Maven 继承

#### 创建父工程

> 创建父工程和普通maven项目一样
>
> - 在创建成功之后再pom.xml添加   
>
> ```xml
>   <packaging>pom</packaging>
> ```
>
> - 删除整个src目录
>
> ![image.png](https://i.loli.net/2020/12/16/Fy2feV7lrNpgDP5.png)

#### 创建子工程

> 在idea中子工程（模块）创建如图
>
> ![image.png](https://i.loli.net/2020/12/16/YtaJu61LIXmVTrE.png)
>
> 创建成功之后pom.xml
>
> ![image.png](https://i.loli.net/2020/12/16/TJg6iLMjUwuqN2v.png)

#### 父工程统一管理jar的版本号

> pom类型工程不直接使用项目依赖的jar
>
> ​	在父工程添加依赖
>
> ```xml
> <!--声明依赖标签-->
>     <dependencyManagement>
>         <dependencies>
>             <dependency>
>                 <groupId>junit</groupId>
>                 <artifactId>junit</artifactId>
>                 <version>4.13.1</version>
>                 <scope>test</scope>
>             </dependency>
>         </dependencies>
>     </dependencyManagement>
> ```
>
> 在子工程使用
>
> ```xml
> <dependencies>
>     <dependency>
>         <groupId>junit</groupId>
>         <artifactId>junit</artifactId>
>         <scope>test</scope>
>     </dependency>
> </dependencies>
> ```
>
> 版本统一
>
> ```xml
> <properties>
>         <!--可以自定义标签-->
>         <junit.version>4.13.1</junit.version>
>     </properties>
>     <!--声明依赖标签-->
>     <dependencyManagement>
>         <dependencies>
>             <dependency>
>                 <groupId>junit</groupId>
>                 <artifactId>junit</artifactId>
>                 <!--使用${名称}-->
>                 <version>${junit.version}</version>
>                 <scope>test</scope>
>             </dependency>
>         </dependencies>
>     </dependencyManagement>
> ```

### Maven 聚合

> 聚合一般一个工程拆分成多个模块开发
>
> 每个模块都是独立的工程，但是运行时必须把所有模块聚合到一起才是一个完成的工程，此时可以使用maven的聚合工程
>
> 电商项目中，包括（商品模块），订单模块，用户模块等---------按业务模块聚合
>
> 表现层，业务层，持久层，分层不同的工程，最后打包是聚合到一起----------架构上的聚合





