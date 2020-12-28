## 1.安裝nginx的依赖

```shell
yum install gcc-c++
#解析nginx的正则
yum -y install pcre pcre-devel
#依赖压缩
yum -y install zlib zlib-devel
#配置ssl
yum install -y openssl openssl-devel
```

## 2.在官网下载安装包 解压

> [nginx官网](https://nginx.org/en/download.html)
>
> ```shell
> #解压
> tar -xzvf 文件tar.gz
> ```
>
> 

## 3.编译

```shell
#切换源码包下          #编译的路径
./configure --prefix=/usr/nginx/nginxopt
#编译检查
make
#编译
make install
```

## 4.常用命令

```shell
cd sbin/
./nginx
./nginx -s stop
./nginx -s quit
./nginx -s reload
./nginx -s quit：此方式停止步骤是待nginx进程处理任务完毕进行停止。
./nginx -s stop：此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。
```

## 5.常见错误

**<span style="color:red">nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)</span>**

> ![image.png](https://i.loli.net/2020/12/26/ZS6W4oh9MaBKegD.png)
>
> ```shell
> #1.执行命令
> fuser -k 80/tcp
> #2.重启nginx
> ./nginx -s reload
> ```

**<span style="color:red">ngixn启动成功，访问不了</span>**

> ```shell
> ps aux|grep nginx
> ```
>
> 执行结果如图：
>
> ![image.png](https://i.loli.net/2020/12/26/5jUP4eRElk19M7W.png)
>
> 然后执行 查看80端口是否分给80端口
>
> ```shell
> netstat -ntlp
> ```
>
> ![image.png](https://i.loli.net/2020/12/26/iTmbjUpJu5Mw62l.png)
>
> 解决办法
> 第一步，对80端口进行防火墙配置：
>
> ```shell
> firewall-cmd --zone=public --add-port=80/tcp --permanent
> ```
>
> 第二步，重启防火墙服务：
>
> ```shell
> systemctl restart firewalld.service
> ```
>
> 如果不行再看阿里云或者腾讯云是否在安全组配置80端口
>
> ![image.png](https://i.loli.net/2020/12/26/kL9pHRoIfqOnFG7.png)