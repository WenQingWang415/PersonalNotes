### 1.下载解压

> [redis官网](https://redis.io/)
>
> ```shell
> #准备工作
> #1.查看gcc版本
> gcc -v
> # 2.如果没安装gcc，执行以下语句
> yum install gcc
> # 如果安装了，执行升级操作
> yum -y install centos-release-scl
> um -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils
> scl enable devtoolset-9 bash
> # 以上为临时启用，如果要长期使用gcc 9.1的话：
> echo "source /opt/rh/devtoolset-9/enable" >>/etc/profile
> #开始
> #1.在官网下载稳定版的上传Linux
> #2.解压
> tar -zxf redis-6.0.9.tar.gz
> ```

### 2.开启端口

> redis的默认端口`6379`
>
> [linux开放端口](https://github.com/WenQingWang415/PersonalNotes/blob/embranchment/Linux/Linux%E9%98%B2%E7%81%AB%E5%A2%99%E5%92%8C%E7%AB%AF%E5%8F%A3.md)

### 3. 安装和编译

> ```shell
> #1. 建立目录  usr/local/redis
> mkdir redis
> #2.安装到/usr/local/redis
> # 进入解压后的目录
> make && make PREFIX=/usr/local/redis install
> ```

### 4.复制配置文件到安装目录对应的文件中

> ```shell
> # 在redis安装目录下，创建etc文件夹
> mkdir usr/local/redis/etc
> # 下载的源码包中复制redis.conf文件到安装目录下新建的etc文件夹下
> cp redis.conf usr/local/redis/etc/
> ```

### 5.启动或者关闭redis

> ```shell
> 使用redis-server命令和指定配置文件来启动
> #1.修改redis.conf文件，将`daemonize no` 改成 `daemonize yes`。
> vim redis.conf
> # 启动redis
> /usr/local/redis/bin/redis-server  /usr/local/redis/etc/redis.conf
> # 关闭redis
> pkill redis
> #查看redis服务是否正常
> # 检查端口号
> netstat -tunpl|grep 6379
> ```

### 6.连接客户端

```shell
#连接         端口
redis-cli -p 6379  #127.0.0.1:6379

#然后输入ping 提示pong代表成功
ping
#输入值
set name WenQingWang 
#取值 
get name
```

### 7.查看redis进程是否开启

```shell
#在开一个Linux连接端口输入
ps -ef|grep redis
#提示如下
```

![image.png](https://wwq-notes.oss-cn-guangzhou.aliyuncs.com/nN2YItOXZySj3bR.png)