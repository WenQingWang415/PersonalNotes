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

