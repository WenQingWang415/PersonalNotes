### 部署war应用

## 1.war包上传

> war上传到Tomcat→webapps

## 2.重启服务

```shell
[root@10 apache-tomcat-9.0.37]# cd bin/
[root@10 bin]# ./shutdown.sh
[root@10 bin]# ./startup.sh
```

## 3.访问

> 默认访问路径是 Ip:8080/productName

## 如何去掉productName 这层路径

> 修改conf→server.xml

![image.png](https://i.loli.net/2020/12/25/nGvzpgfj5CbVOiu.png)

```shell
<Context path="" docBase="solomon" reloadable="true"></Context>

#docBase要改成你的项目目录。
#path为虚拟路径,访问时的路径，注意:不是根目录的，如果是其他路径比如"/test"一定要加"/"" debug建议设置为0
#reloadable设置为true

<Context path="/test" docBase="jenkins" reloadable="true"></Context>
```

### 重启服务

```shell
[root@10 apache-tomcat-9.0.37]# cd bin/
[root@10 bin]# ./shutdown.sh
[root@10 bin]# ./startup.sh
```

