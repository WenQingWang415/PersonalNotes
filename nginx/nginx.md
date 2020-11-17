## Nginx

### 目录说明

#### Windows

```nginx
conf目录：存放配置文件的目录，包含主配置文件nginx.conf，是我们经常修改的配置文件。
contrib目录：存放开源爱好者共享的代码。
docs目录：存放文档资料。
html目录：默认存放了Nginx的错误页面和欢迎页面。
logs目录：默认存放了访问日志、错误日志和Nginx主进程pid文件。
temp目录：临时目录，用于存放Nginx运行时产生的临时文件。
nginx.exe:可执行程序，常用于Nginx服务的启动、停止等管理工作。
```

#### linux：

```nginx
*_temp目录：共有5个temp结尾的目录，用于存放Nginx运行时产生的临时文件。
conf目录：存放配置文件的目录，包含主配置文件nginx.conf，是我们经常修改的配置文件。
html目录：默认存放了Nginx的错误页面和欢迎页面等。
logs目录：默认存放了访问日志和错误日志文件。
sbin目录：默认存放了Nginx的二进制命令，常用于Nginx服务的启动、停止等管理工作。
```

### 常用的命令

```nginx
nginx -s stop ：快速关闭Nginx，可能不保存相关信息，并迅速终止web服务。
nginx -s quit ：平稳关闭Nginx，保存相关信息，有安排的结束web服务。
nginx -s reload ：因改变了Nginx相关配置，需要重新加载配置而重载。
nginx -s reopen ：重新打开日志文件。
nginx -c filename ：为 Nginx 指定一个配置文件，来代替缺省的。
nginx -t ：不运行，而仅仅测试配置文件。nginx 将检查配置文件的语法的正确性，并尝试打开配置文件中所引用到的文件。
nginx -v：显示 nginx 的版本。
nginx -V：显示 nginx 的版本，编译器版本和配置参数。

rem 如果启动前已经启动nginx并记录下pid文件，会kill指定进程
nginx.exe -s stop

rem 测试配置文件语法正确性
nginx.exe -t -c conf/nginx.conf

rem 按照指定配置去启动nginx
nginx.exe -c conf/nginx.conf
我一般使用这个启动
```

### Nginx配置文件说明

```nginx

```

