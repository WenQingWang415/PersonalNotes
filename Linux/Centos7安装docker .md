## 一、安装前必读

在安装 Docker 之前，先说一下配置，我这里是Centos7 Linux 内核：官方建议 3.10 以上，3.8以上貌似也可。

注意：本文的命令使用的是 root 用户登录执行，不是 root 的话所有命令前面要加 `sudo`

**1.查看当前的内核版本**

```shell
uname -r
```

![image.png](https://i.loli.net/2020/12/24/MihpSl38ytbOT6J.png)

**2.卸载旧版本（如果之前安装过的话）**

```shell
yum -y remove docker docker-common docker-selinux docker-engine
```

![image.png](https://i.loli.net/2020/12/24/a5oX6VZEuRKnIby.png)

## 二、安装Docker的详细步骤

[docker官网](https://docs.docker.com/)

**1.安装需要的软件包， yum-util 提供yum-config-manager功能，另两个是devicemapper驱动依赖**

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
```

![image.png](https://i.loli.net/2020/12/24/gl6E8smWzHMtTVc.png)

**2.设置 yum 源**

[阿里云yum源官网](https://developer.aliyun.com/mirror/)→容器→docker-ce

设置一个yum源

```shell
yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

![image.png](https://i.loli.net/2020/12/24/PxFwAIqGSkyplVY.png)

**3.更新并安装Docker-CE**

```shell
 yum makecache fast
 yum -y install docker-ce
```

**4.启动Docker**

```shell
systemctl start docker
或者
service docker start
```

**5.校验**

```shell
docker version
```

![image.png](https://i.loli.net/2020/12/24/2QPOyzvKHh8qDBk.png)

