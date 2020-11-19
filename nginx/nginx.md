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

### 语法说明

#### Location

##### 语法规则

```nginx
location [=|~|~*|^~] /uri/ {… }
```

- 首先匹配 =
- 其次匹配^~
- 其次是按文件中顺序的正则匹配
- 最后是交给 /通用匹配
- 当有匹配成功时候，停止匹配，按当前匹配规则处理请求

##### 符号含义

```nginx
#表示精确匹配
=
#表示uri以某个常规字符串开头，理解为匹配 url路径即可
#nginx不对url做编码，因此请求为/static/20%/aa，可以被规则^~ /static/ /aa匹配到（注
意是空格）
^~
#表示区分大小写的正则匹配
~
#表示不区分大小写的正则匹配
~*
#!~和!~*分别为区分大小写不匹配及不区分大小写不匹配的正则
!~和!~*
#用户所使用的代理（一般为浏览器）
/
#可以记录客户端IP，通过代理服务器来记录客户端的ip地址
$http_x_forwarded_for
#可以记录用户是从哪个链接访问过来的
$http_referer
```

##### 常用规则

- 直接匹配网站根，通过域名访问网站首页比较频繁，使用这个会加速处理

第一个必选规则

```nginx
location = / {
proxy_pass http://tomcat:8080/index
}
```

第二个必选规则是处理静态文件请求，这是nginx作为http服务器的强项

- 有两种配置模式，目录匹配或后缀匹配,任选其一或搭配使用

```nginx
location ^~ /static/ {
# 请求/static/a.txt 将被映射到实际目录文件:/webroot/res/static/a.txt
root /webroot/res/;
}
location ~* \.(gif|jpg|jpeg|png|css|js|ico)${
root /webroot/res/;
}
```

第三个规则就是通用规则，用来转发动态请求到后端应用服务器

```nginx
location / {
proxy_pass http://tomcat:8080/
}
```

##### 总结

- 先判断精准命中，如果命中，立即返回结果并结束解析过程
- 判断普通命中，如果有多个命中，“记录”下来“最长”的命中结果（记录但不结束，最长的为准）
- 继续判断正则表达式的解析结果，按配置里的正则表达式顺序为准，由上至下开始匹配，一旦匹配 成功1个，立即返回结果，并结束解析过程
- 普通命中顺序无所谓，是因为按命中的长短来确定。正则命中，顺序有所谓，因为是从前入往后命 中的

#### ReWrite

- rewrite只能放在server{},location{},if{}中 ，并且只能对域名后边的除去传递的参数外的字符串起 作用
- Nginx提供的全局变量或自己设置的变量，结合正则表达式和标志位实现url重写以及重定向
- Rewrite主要的功能就是实现URL的重写
- Nginx的Rewrite规则采用Pcre，perl兼容正则表达式的语法规则匹配，如果需要Nginx的Rewrite 功能，在编译Nginx之前，需要编译安装PCRE库
- 通过Rewrite规则，可以实现规范的URL、根据变量来做URL转向及选择配置

##### 相关指令

- break ：
  - [ ] 默认值 ：none
  - [ ] 使用范围 ：if，server，location
  - [ ] 作用 ：完成当前的规则集，不再处理rewrite指令，需要和last加以区分
- if ( condition ) {....}
  - [ ] 默认值 ：none
  - [ ] 使用范围 ：server，location
  - [ ] 作用：用于检测一个条件是否符合，符合则执行大括号内的语句。不支持嵌套，不支持多个 条件&&或||处理
- return
  - [ ] 默认值 ：none
  - [ ] 使用范围 ：server，if，location
  - [ ] 作用：用于结束规则的执行和返回状态码给客户端
- rewrite regex replacement flag
  - [ ] 使用范围 ：server，if，location
  - [ ] 作用：该指令根据表达式来重定向URI，或者修改字符串。指令根据配置文件中的顺序来执 行。注意重写表达式只对相对路径有效
- uninitialized_variable_warn on|of
  - [ ] 默认值 ：on
  - [ ] 使用范围：http,server,location,if
  - [ ] 作用：该指令用于开启和关闭未初始化变量的警告信息，默认值为开启
- set variable value
  - [ ] 默认值 ：none
  - [ ] 作用：该指令用于定义一个变量，并且给变量进行赋值。变量的值可以是文本、一个变量或 者变量和文本的联合，文本需要用引号引起来

##### rewrite全局变量表

| 变量              |                             含义                             |
| :---------------- | :----------------------------------------------------------: |
| $args             |         这个变量等于请求行中的参数，同$query_string          |
| $content length   |                请求头中的Content-length字段。                |
| $content_type     |                 请求头中的Content-Type字段。                 |
| $document_root    |                当前请求在root指令中指定的值。                |
| $host             |              请求主机头字段，否则为服务器名称。              |
| $http_user_agent  |                       客户端agent信息                        |
| $http_cookie      |                       客户端cookie信息                       |
| $limit_rate       |                  这个变量可以限制连接速率。                  |
| $request_method   |             客户端请求的动作，通常为GET或POST。              |
| $remote_addr      |                       客户端的IP地址。                       |
| $remote_port      |                        客户端的端口。                        |
| $remote_user      |           已经经过Auth Basic Module验证的用户名。            |
| $request_filename |     当前请求的文件路径，由root或alias指令与URI请求生成。     |
| $scheme           |                 HTTP方法（如http，https）。                  |
| $server_protocol  |          请求使用的协议，通常是HTTP/1.0或HTTP/1.1。          |
| $server_addr      |       服务器地址，在完成一次系统调用后可以确定这个值。       |
| $server_name      |                         服务器名称。                         |
| $server_port      |                   请求到达服务器的端口号。                   |
| $request_uri      | 包含请求参数的原始URI，不包含主机名，如”/foo/bar.php?arg=baz”。 |
| $uri              | 不带请求参数的当前URI，$uri不包含主机名，如”/foo/bar.html”。 |
| $document_uri     |                         与$uri相同。                         |

##### 语法规则：

| 操作符  |                             含义                             |
| ------- | :----------------------------------------------------------: |
| = ,!=   |                   比较的一个变量和字符串。                   |
| ~， ~*  | 与正则表达式匹配的变量，如果这个正则表达式中包含}，;则整个表达式需要用"或'包围。 |
| -f，!-f |                    检查一个文件是否存在。                    |
| -d, !-d |                    检查一个目录是否存在。                    |
| -e，!-e |            检查一个文件、目录、符号链接是否存在。            |



##### IF指令：

```nginx
if 语法格式
if 空格 (条件) {
重写模式
}
# 限制浏览器访问
if ($http_user_agent ~ Firefox) {
rewrite ^(.*)$ /firefox/$1 break;
}
if ($http_user_agent ~ MSIE) {
rewrite ^(.*)$ /msie/$1 break;
}
if ($http_user_agent ~ Chrome) {
rewrite ^(.*)$ /chrome/$1 break;
}

```

##### return指令：

```nginx
# 限制IP访问
if ($remote_addr = 192.168.197.142) {
return 403;
}
```

- [ ]  首先从日志查出ip
- [ ] 修改conf配置文件
- [ ] 重启配置

##### rewrite指令：

- [ ] 判断目录是否存在
- [ ] 服务器内部的rewrite和302跳转不一样.跳转的话URL都变了,变成重新http请求index.html,而内部 rewrite,上下文没变

```nginx
if (!-e $document_root$fastcgi_script_name) {
rewrite ^.*$ /index.html break;
}
```

##### set指令：

- [ ] set指令是设置变量用的,可以用来达到多条件判断时作标志用
- [ ] 判断IE并重写,且不用break;我们用set变量来达到目的

### 运行过程

#### 默认情况下，运行中的Nginx会包含如下进程：

- 主进程master process（父进程）
  - [ ] 主进程充当监控进程
  - [ ] 负责整个进程组与管理用户的交互接口，同时对进程进行监护
  - [ ] 它不需要处理网络事件，不负责业务执行，只会通过管理worker进程来实现重启服务、关闭 服务、配置文件生效等功能
- 子进程worker process（工作进程）
  - [ ] 子进程充当工作进程
  - [ ] 负责完成具体的任务
  - [ ] 完成用户请求接收与返回用户数据，以及与后端应用服务器的数据交互等工作

#### 原理介绍：

- Nginx 的高并发得益于其采用了 epoll 模型，与传统的服务器程序架构不同，epoll 是linux 内核 2.6 以后才出现的
- Nginx 采用 epoll 模型，异步非阻塞，而 Apache 采用的是select 模型
  - [ ] Select 特点：select 选择句柄的时候，是遍历所有句柄，也就是说句柄有事件响应时，select 需要遍历所有句柄才能获取到哪些句柄有事件通知，因此效率是非常低
  - [ ] epoll 的特点：epoll 对于句柄事件的选择不是遍历的，是事件响应的，就是句柄上事件来就 马上选择出来，不需要遍历整个句柄链表，因此效率非常高

### Nginx配置文件说明

```nginx

```

### 代理模式

#### 1.正向代理

> 正向代理（forward proxy）：是一个位于客户端(用户A)和原始服务器(origin server)(目标服务器)之间的服务器(代理服务器)，为了从原始服务器取得内容，客户端向代理服务器发送一个请求并指定目标(原始服务器)，然后代理服务器向原始服务器转交请求并将获得的内容返回给客户端。客户端必须要进行一些特别的配置才能使用正向代理。一般情况下，如果没有特别说明，代理技术默认是指正向代理技术。
>



从上面的概念中，我们可以知道，所谓的正向代理，就是代理服务器替代客户端(用户A)，来访问原始服务器(目标服务器)。

**举个例子：**

　　我是一个用户，我访问不了某网站，但是我能访问一个代理服务器，这个代理服务器呢,他能访问那个我不能访问的网站，于是我先连上代理服务器,告诉他我需要那个无法访问网站的内容，代理服务器去取回来,然后返回给我。从网站的角度，只在代理服务器来取内容的时候有一次记录，有时候并不知道是用户的请求，也隐藏了用户的资料，这取决于代理告不告诉网站。

**还不懂？看下图：**

![image-20201117160938187](https://i.loli.net/2020/11/17/UdxcYTkClfOHrqm.png)



#####1.1正向代理的作用：

###### **访问本来无法访问的资源**

![image-20201117162748551](https://i.loli.net/2020/11/17/ksm5bGASv9FI1KP.png)

我们抛除复杂的网络路由情节来看图，图中路由器从左到右为R1,R2假设最初用户A要访问目标服务器需要经过R1和R2路由器这样一个路由节点，如果路由器R1或者路由器R2发生故障，那么就无法访问目标服务器了。但是如果用户A让代理服务器去代替自己访问目标服务器，由于代理服务器没有在路由器R1或R2节点中，而是通过其它的路由节点访问目标服务器，那么用户A就可以得到目标服务器的数据了。现实中的例子就是“翻墙”。不过自从VPN技术被广泛应用外，“翻墙”不但使用了传统的正向代理技术，有的还使用了VPN技术。

**可以做缓存，加速访问资源**

  主要是提高代理服务器的宽带流量，目前不流行了。

  Cache（缓存）技术和代理服务技术是紧密联系的（不光是正向代理，反向代理也使用了Cache（缓存）技术。还如上图所示，如果在用户A访问目标服务器某数据之前，已经有人通过代理服务器访问过目标服务器上得数据，那么代理服务器会把数据保存一段时间，如果有人正好取该数据，那么代理服务器不再访问目标服务器，而把缓存的数据直接发给用户A。这一技术在Cache中术语就叫Cache命中。如果有更多的像用户A的用户来访问代理服务器，那么这些用户都可以直接从代理服务器中取得数据，而不用千里迢迢的去目标服务器下载数据了。

**对客户端访问授权，上网进行认证**

![image-20201117170137376](https://i.loli.net/2020/11/17/5DoimvAGgE6TkrL.png)

防火墙作为网关，用来过滤外网对其的访问。假设用户A和用户B都设置了代理服务器，用户A允许访问互联网，而用户B不允许访问互联网（这个在代理服务器上做限制）这样用户A因为授权，可以通过代理服务器访问到目标服务器，而用户B因为没有被代理服务器授权，所以访问目标服务器时，数据包会被直接丢弃。

**代理可以记录用户访问记录（上网行为管理），对外隐藏用户信息**



![image-20201117170303660](https://i.loli.net/2020/11/17/MbC8sfg76c2a3RL.png)

目标服务器并不知道访问自己的实际是用户A，因为代理服务器代替用户A去直接与目标服务器进行交互。如果代理服务器被用户A完全控制（或不完全控制），会惯以“肉鸡”术语称呼

#### 2.反向代理

 反向代理（reverse proxy）：和正向代理正好相反，对于客户端而言它就像是原始服务器，并且客户端不需要进行任何特别的设置。客户端向反向代理的命名空间(name-space)中的内容发送普通请求，接着反向代理将判断向何处(原始服务器)转交请求，并将获得的内容返回给客户端，就像这些内容原本就是它自己的一样。

#####反向代理的作用：

**1：保证内网的安全，可以使用反向代理提供WAF功能，阻止web攻击**

  ==(大型网站，通常将反向代理作为公网访问地址，Web服务器是内网)==

![image-20201118080505653](https://i.loli.net/2020/11/18/KNYSjGVpzRfQrxn.png)

用户A始终认为它访问的是目标服务器而不是代理服务器，但实用际上反向代理服务器接受用户A的应答，从目标服务器中取得用户A的需求资源，然后发送给用户A。由于防火墙的作用，只允许代理服务器访问目标服务器。尽管在这个虚拟的环境下，防火墙和反向代理的共同作用保护了目标服务器，但用户A并不知情。

**2：负载均衡，通过反向代理服务器来优化网站的负载**

![image-20201118080746897](https://i.loli.net/2020/11/18/DBZopVGLTIgvYW8.png)

当反向代理服务器不止一个的时候，我们甚至可以把它们做成集群，当更多的用户访问目标服务器的时候，让不同的代理服务器去应答不同的用户，然后发送不同用户需要的资源。



#### 3.透明代理

透明代理：透明代理的意思是客户端根本不需要知道有代理服务器的存在，它改编你的request fields（报文），并会传送真实IP。注意，加密的透明代理则是属于匿名代理，意思是不用设置使用代理了。 透明代理实践的例子就是时下很多公司使用的行为管理软件

### Nginx如何配置正向代理和反向代理

#### 1.正向代理

```nginx
server{
        resolver 10.1.23.4;
        resolver_timeout 30s; 
        listen 8888;
        location / {
                proxy_pass http://$http_host$request_uri;
                proxy_set_header Host $http_host;
                proxy_buffers 256 4k;
                proxy_max_temp_file_size 0;
                proxy_connect_timeout 30;
                proxy_cache_valid 200 302 10m;
                proxy_cache_valid 301 1h;
                proxy_cache_valid any 1m;
        }
}
```

> 注意：
>
> 1：不能有hostname
>
> 2：必须有resolver, 即dns，超时时间可选项
>
> 3：配置缓存大小，关闭磁盘缓存读写减少I/O、代理连接超时时间
>
> 4：配置代理服务器 Http 状态缓存时间
>
> 配置好后，重启nginx，以浏览器为例，要使用这个代理服务器，则只需将浏览器代理设置为http://IP:8888，即可使用了。

#### 2.反向代理

```nginx
http {
#省略了前面一般的配置，直接从负载均衡这里开始
#设置地址池，后端3台服务器
 upstream servermap {
        server 192.168.1.1:8080 weight=2 max_fails=2 fail_timeout=30s;
        server 192.168.1.2:8080 weight=3 max_fails=2 fail_timeout=30s;
        server 192.168.1.38080 weight=4 max_fails=2 fail_timeout=30s;
    }
#一个虚拟主机，用来反向代理http_server_pool这组服务器
	server {
        listen       80;
#外网访问的域名        
        server_name  www.test.com; 
        location / {
# 后端服务器返回500 503 404错误，自动请求转发到upstream池中另一台服务器
            proxy_next_upstream error timeout invalid_header http_500 http_503 http_404;
            proxy_pass http://servermap;
            proxy_set_header Host www.test.com;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For  $proxy_add_x_forwarded_for;
        }
        access_log  logs/www.test.com.access.log  combined;
    }
}
```

### Nginx负载均衡

#### 1.轮询法（默认）

> 将请求按顺序轮流的分配到后端服务器上，它将均衡的对待后端的每一台服务器，而不关心服务器的实际连接数和当前的系统负载

```nginx
http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
    #注意 加了upstream 就是代表负载均衡， 
    ##
	upstream localhost{
        #要做负载均衡的IP或者域名
	   server 192.168.43.21:8030;
	     server 192.168.43.29:8031;
		   server 192.168.2.150:8032;
		     server 192.168.2.132:8035;
	   
	} 
    server {
        listen       8090;
        server_name  localhost;
        location / {
           # root   html;
            #index  index.html index.htm;
			 proxy_pass   http://localhost;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
       
    }

}
```

说明：

![image-20201118105426025](https://i.loli.net/2020/11/18/1SGADikBP39OcUg.png)

#### 2.加权轮询发（weight）

> - 不同的后端服务器可能机器的配置和当前的系统的负载并不相同，因此他们的抗压能力也不同
> - 给配置越高的权重越高，可以处理更多的请求
> - 配置低，负载高的机器，分配低的权重，降低其系统的负载
> - 加权轮询能更好的将请求按照权重分配到后端
> - weight 越大分配的权限就就越高，访问量越大

```nginx
http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
    #注意 加了upstream 就是代表负载均衡， 
    #weight=10 值越大访问的的次数就越多
	upstream localhost{
        #要做负载均衡的IP或者域名
	   server 192.168.43.21:8030 weight=10;
	     server 192.168.43.29:8031 weight=8;
		   server 192.168.2.150:8032 weight=5;
		     server 192.168.2.132:8035 weight=2;
	   
	} 
    server {
        listen       8090;
        server_name  localhost;
        location / {
           # root   html;
            #index  index.html index.htm;
			 proxy_pass   http://localhost;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
       
    }

}
```

#### 3.原地址哈希法(ip_hash)

> - 通过获取客户端的IP地址，通过哈希函数计算得到一个数值
> - 用该数值对服务器列表的大小进行摸运算，得到的结果便是客户端要访问的服务器的序号
> - 采用原地址哈希进行负载均衡，同一地址的客户端，当服务器列表不变时，它每次都会映射到同一台服务器进行访问。
> - 可以保证来自同一IP的请求被打到固定的机器上，可以解决session的问题（有的时候session会对不上，建议使用认证或者Redis）

```nginx
http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
    #注意 加了upstream 就是代表负载均衡， 
    #weight=10 值越大访问的的次数就越多
	upstream localhost{
        #要做负载均衡的IP或
        ip_hash;
	   server 192.168.43.21:8030 ;
	     server 192.168.43.29:8031 ;
		   server 192.168.2.150:8032 ;
		     #server 192.168.2.132:8035 ;
		     #如果注释掉在访问的会自动变化
	   
	} 
    server {
        listen       8090;
        server_name  localhost;
        location / {
           # root   html;
            #index  index.html index.htm;
			 proxy_pass   http://localhost;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
       
    }

}
```

#### 4.最小连接数法（least_conn）

> 由于每台的服务器配置各不相同，对请求的处理速度有快慢，最小连接数根据后端服务器当前的情况，动态选择最小的连接数，来处理当前的请求，尽可能的提高后端服务器的效率，将负责合理分流每一台服务器

```nginx
http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;
    #注意 加了upstream 就是代表负载均衡， 
    #weight=10 值越大访问的的次数就越多
	upstream localhost{
        #要做负载均衡的IP
        
      least_conn;
            
	   server 192.168.43.21:8030 ;
	     server 192.168.43.29:8031 ;
		   server 192.168.2.150:8032;
		     #server 192.168.2.132:8035;
		     #如果注释掉在访问的会自动变化
	   
	} 
    server {
        listen       8090;
        server_name  localhost;
        location / {
           # root   html;
            #index  index.html index.htm;
			 proxy_pass   http://localhost;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
       
    }

}
```

​                                                            ==以下两种在linux系统上使用，windows系统不支持，以下两种没有测试==

#### 5.Fair

根据后端服务器的响应时间来分配请求，响应时间短的优先分配（比weight、ip_hash更智能的负载均衡算法。需安装upsteram_fair模块）

> linux下安装fair
>
> 下载地址：https://github.com/gnosek/nginx-upstream-fair
>
> 解压：unzip   nginx-upsiream-fair-master.zip
>
> ---prefix编译opt目录 编译皱增加add-module模块
>
> 增加模块： ./configure --prefix=/opt/nginx --add-module=/opt/nginx-upstream-fair-master
>
> defalut_port问题修改：cd  nginx-upsiream-fair-master
>
> sed -i 's/default_port/no_port/g' ngx_http_upstream_fair_module.c
>
> make
>
> make install

```nginx
upstream tomcat_server {
    fair;
    server 192.168.10.11:8080 weight=1;
    server 192.168.10.12:8080 weight=1;
}
```



#### 6.url_hash

url_hash：按访问的URL的哈希结果来分配请求，使每个URL定向到一台后端服务器（提高后端缓存服务器的效率，需安装Nginx的hash软件包）

> 下载地址：https://github.com/evanmiller/nginx_upstream_hash
>
> 解压zip：unzip nginx_upstream_hash-master.zip
>
>  增加模块： ./configure --prefix=/opt/nginx --add-module=/opt/ nginx_upstream_hash-master
>
> make
>
> make install

```nginx
upstream tomcat_server {
    hash $request_uri;
    server 192.168.10.11:8080 weight=1;
    server 192.168.10.12:8080 weight=1;
}
```



### 日志管理和日志分割(linux)

#### 日志管理

通过访问日志，你可以得到用户地域来源、跳转来源、使用终端、某个URL访问量等相关信息

 通过错误日志，你可以得到系统某个服务或server的性能瓶颈等

#### 日志格式

日志生成的到Nginx根目录logs/access.log文件，默认使用“main”日志格式，也可以自定义格式 

默认“main”日志格式

```nginx
log_format main '$remote_addr - $remote_user [$time_local] "$request" '
'$status $body_bytes_sent "$http_referer" '
'"$http_user_agent" "$http_x_forwarded_for"';
$remote_addr：客户端的ip地址(代理服务器，显示代理服务ip)
$remote_user：用于记录远程客户端的用户名称（一般为“-”）
$time_local：用于记录访问时间和时区
$request：用于记录请求的url以及请求方法
$status：响应状态码，例如：200成功、404页面找不到等。
$body_bytes_sent：给客户端发送的文件主体内容字节数
$http_user_agent：用户所使用的代理（一般为浏览器）
$http_x_forwarded_for：可以记录客户端IP，通过代理服务器来记录客户端的ip地址
$http_referer：可以记录用户是从哪个链接访问过来的
```

#### 日志切割

nginx的日志文件没有rotate功能

编写每天生成一个日志，我们可以写一个nginx日志切割脚本来自动切割日志文件

第一步就是重命名日志文件 （不用担心重命名后nginx找不到日志文件而丢失日志。在你未 重新打开原名字的日志文件前，nginx还是会向你重命名的文件写日志，Linux是靠文件描述 符而不是文件名定位文件 ）

第二步向nginx主进程发送USR1信号

- nginx主进程接到信号后会从配置文件中读取日志文件名称
- 重新打开日志文件 (以配置文件中的日志名称命名) ，并以工作进程的用户作为日志文件 的所有者
- 重新打开日志文件后，nginx主进程会关闭重名的日志文件并通知工作进程使用新打开 的日志文件
- 工作进程立刻打开新的日志文件并关闭重名名的日志文件
- 然后你就可以处理旧的日志文件了。[或者重启nginx服务]

nginx日志按每分钟自动切割脚本如下 ：

新建shell脚本：

```nginx
vi /opt/nginx/nginx_log.sh
```

复制到脚本里面

```nginx
#!/bin/bash
#设置日志文件存放目录
LOG_HOME="/opt/nginx/logs/"
#备分文件名称
LOG_PATH_BAK="$(date -d yesterday +%Y%m%d%H%M)".access.log
#重命名日志文件
mv ${LOG_HOME}/access.log ${LOG_HOME}/${LOG_PATH_BAK}.log
#向nginx主进程发信号重新打开日志
kill -USR1 `cat /opt/nginx/logs/nginx.pid`

```

创建crontab设置作业

设置日志文件存放目录crontab -e

   cron表达式:  https://cron.qqe2.com/

```ngin
*/1 * * * * sh /opt/nginx/nginx_log.sh
```

   重新启动定时任务

```nginx
service crond restart
```



### 动静分离





##### 实现：

- 通过 location 指定不同的后缀名实现不同的请求转发
- 通过 expires 参数设置，可以使浏览器缓存过期时间，减少与服务器之前的请求和流量
  - [ ] Expires 定义：是给一个资源设定一个过期时间，也就是说无需去服务端验证，直接通 过浏览器自身确认是否过期即可，所以不会产生额外的流量 
  - [ ] 此种方法非常适合不经常变动的资源。（如果经常更新的文件，不建议使用 Expires 来 缓存） 
  - [ ] 这里设置 3d，表示在这 3 天之内访问这个 URL，发送一个请求，比对服务器该文件最 后更新时间没有变化，则不会从服务器抓取，返回状态码 304，如果有修改，则直接从 服务器重新下载，返回状态码 200

##### 示例：

- 新建一个web工程，并设置一张图片
- 修改nginx配置文件：

```nginx
server {
listen 80;
server_name a;
location ~ .*\.(html|htm|gif|jpg|jpeg|bmp|png|ico|txt|js|css)$
{
        #G:/nginx-1.18.0/static; 全路径
root /opt/apache-tomcat-8.5.31/webapps/;
expires 30d;
}
}
```

### 高并发配置



