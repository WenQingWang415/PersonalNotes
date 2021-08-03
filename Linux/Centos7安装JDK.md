# 1.检查是否有安装jdk

**1.如果有安装openjdk则卸载**

```shell
java -version
```

**2.检查**

```shell
rpm -qa | grep openjdk #openjdk的
rpm -qa|grep jdk
```

**3.删除**

```shell
#卸载 -e --nodeps 强制删除
rpm -e --nodeps #检查中所有的
#在输入
java -version
#提示
java: command not found #则ok
```

# 安装jdk1.8

**1.如果没有wget,则安装**

```shell
yum install wget
```

**2.安装oracle-jdk**

[下载地址](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)

```java
账号：2696671285@qq.com
密码：Oracle123
```

![image.png](https://wwq-notes.oss-cn-guangzhou.aliyuncs.com/AEbGhtgHOB7k1cf.png)

```shell
#下载之后上传
#1.解压
tar -xzvf jdk-8u271-linux-x64.tar.gz
#2.创建/usr/java
mkdir /usr/java
#3.把解压后的文件mv过去
mv jdk1.8.0_271 /usr/java
#然后JAVA_HOME就应该是
/usr/java/jdk1.8.0_271
```

**3.设置环境变量**

```shell
#1.打开文件修改
vi /etc/profile

# 2.最下面加入这几行（环境变量的设置跟openjdk没啥区别，只有第一行的路径不同而已）
JAVA_HOME=/usr/java/jdk1.8.0_271
JRE_HOME=$JAVA_HOME/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH

#3.让设置生效
source /etc/profile

#4.测试 java -version
java version "1.8.0_271"
Java(TM) SE Runtime Environment (build 1.8.0_271-b09)
Java HotSpot(TM) 64-Bit Server VM (build 25.271-b09, mixed mode)

```

