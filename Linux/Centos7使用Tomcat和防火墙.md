#### **1.在官网下载Tomcat压缩包**

[Tomact官网](http://tomcat.apache.org/)

#### **2.压缩**

```shell
#1.把下载好的压缩包上传服务器
#2.创建创建/usr/tomcat
mkdir /usr/tomcat
#3.解压
tar -xzvf apache-tomcat-9.0.41.tar.gz
#4.移动usr/tomcat目录下
mv apache-tomcat-9.0.41 /usr/tomcat
```

#### **3.启动**

```shell
# 执行：startup.sh -->启动tomcat
# 执行：shutdown.sh -->关闭tomcat
./startup.sh
./shutdown.sh
```





#### **4.测试：**

```shell
输入ip+8080即可访问
```

#### 防火墙

**<span style="color:red">注意：确保Linux的防火墙端口是开启的，如果是阿里云，需要保证阿里云的安全组策略是开放的！</span>**

```shell
# 查看firewall服务状态
systemctl status firewalld

# 开启、重启、关闭、firewalld.service服务
# 开启
service firewalld start
# 重启
service firewalld restart
# 关闭
service firewalld stop

# 查看防火墙规则
firewall-cmd --list-all    # 查看全部信息
firewall-cmd --list-ports  # 只看端口信息

# 开启端口
开端口命令：firewall-cmd --zone=public --add-port=80/tcp --permanent
重启防火墙：systemctl restart firewalld.service

命令含义：
--zone #作用域
--add-port=80/tcp  #添加端口，格式为：端口/通讯协议
--permanent   #永久生效，没有此参数重启后失效
```

#### 在同一台服务器下运行多个Tomact

> ```shell
> #打开文件编辑环境变量
> vim /etc/profile
> 
> #第一台tomact
> CATALINA_BASE=/usr/tomcat/tomcat9
> 
> CATALINA_HOME=/usr/tomcat/tomcat9
> 
> TOMCAT_HOME=/usr/tomcat/tomcat9
> 
> export CATALINA_BASE CATALINA_HOME TOMCAT_HOME
> 
> #第二台tomact
> CATALINA_2_BASE=/usr/tomcat/tomcat9.0
> 
> CATALINA_2_HOME=/usr/tomcat/tomcat9.0
> 
> TOMCAT_2_HOME=/usr/tomcat/tomcat9.0
> 
> export CATALINA_2_BASE CATALINA_2_HOME TOMCAT_2_HOME
> 
> #保存退出。
> 
> #再输入：
> source /etc/profile
> 
> #才能生效。
> 
> #第一个tomcat，保持解压后的原状不用修改, 来到第二个tomcat的bin目录下
> 打开catalina.sh ，找到下面红字，
> 
>  # OS specific support.  $var _must_ be set to either true or false.
> 
> #在下面增加如下代码
> 
> export CATALINA_BASE=$CATALINA_2_BASE
> 
> export CATALINA_HOME=$CATALINA_2_HOME
> 
> export CATALINA_BASE=$CATALINA_BASE
> 
> export CATALINA_HOME=$CATALINA_HOME
> #保存
> #然后重启两个Tomact
> ```
>
> 