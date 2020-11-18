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

```ngin
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
        ip_hash;
	   server 192.168.43.21:8030 weight=10;
	     server 192.168.43.29:8031 weight=8;
		   server 192.168.2.150:8032 weight=5;
		     #server 192.168.2.132:8035 weight=2;
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

```





#### 5.Fair



#### 6.url_hash



### 日志管理和日志分割

### 动态分离





