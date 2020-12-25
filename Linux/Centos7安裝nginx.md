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

## 3.编译

```shell
#切换源码包下          #编译的路径
./configure --prefix=/usr/nginx/nginxopt
#编译检查
make
#
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

