#### **1.在官网下载Tomcat压缩包**

[Tomact官网](http://tomcat.apache.org/)

#### **2.压缩**

```
＃ 1.把下载好的压缩包上传服务器
＃ 2.创建创建/ usr / tomcat
mkdir / usr / tomcat
＃ 3.解压
tar -xzvf apache-tomcat-9.0.41.tar.gz
＃ 4.移动usr / tomcat目录下
mv apache-tomcat-9.0.41 / usr / tomcat
```

#### **3.启动**

```
＃执行：startup.sh->启动tomcat 
＃执行：shutdown.sh->关闭tomcat
./startup.sh
./shutdown.sh
```

#### **4.测试：**

```
输入ip + 8080可访问
```

#### 在同一台服务器下运行多个Tomact

> ```
> ＃打开文件编辑环境变量
> vim / etc / profile
> 
> ＃第一台tomact
> CATALINA_BASE = / usr / tomcat / tomcat9
> 
> CATALINA_HOME = / usr / tomcat / tomcat9
> 
> TOMCAT_HOME = / usr / tomcat / tomcat9
> 
> 导出CATALINA_BASE CATALINA_HOME TOMCAT_HOME
> 
> ＃第二台tomact
> CATALINA_2_BASE = / usr / tomcat / tomcat9.0
> 
> CATALINA_2_HOME = / usr / tomcat / tomcat9.0
> 
> TOMCAT_2_HOME = / usr / tomcat / tomcat9.0
> 
> 导出CATALINA_2_BASE CATALINA_2_HOME TOMCAT_2_HOME
> 
> ＃保存退出。
> 
> ＃再输入：
> source / etc / profile
> 
> ＃才能发挥。
> 
> ＃第一个tomcat，保持解压后的原状不用修改，来到第二个tomcat的bin目录下
> ：catalina.sh，找到以下红字，
> 
>  ＃特定于操作系统的支持。必须将$ var设置为true或false。
> 
> ＃在下面增加如下代码
> 
> 出口CATALINA_BASE = $ CATALINA_2_BASE
> 出口CATALINA_HOME = $ CATALINA_2_HOME
> 
> ＃保存
> ＃然后重启两个Tomact
> ```
>
> 修改端口上面的没有配置
>
> [![image.png](https://camo.githubusercontent.com/7bdaa4a5f6f6227517618880023a498e788fe5e2b851b289c113d7e1aee364c3/68747470733a2f2f692e6c6f6c692e6e65742f323032302f31322f32382f6d54414b624a4361487a67564f44582e706e67)](https://camo.githubusercontent.com/7bdaa4a5f6f6227517618880023a498e788fe5e2b851b289c113d7e1aee364c3/68747470733a2f2f692e6c6f6c692e6e65742f323032302f31322f32382f6d54414b624a4361487a67564f44582e706e67)