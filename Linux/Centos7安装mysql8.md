## Mysql安装

### 1.添加包

```shell
wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
rpm -ivh mysql80-community-release-el7-3.noarch.rpm
```

### 2.更新 yum 命令

```shell
yum clean all && yum makecache
```

### 3.安装

```shell
yum install -y mysql-community-server
```

### 4.启动服务

```shell
#启动服务
systemctl start mysqld

#查看版本信息
mysql -V

#查看状态
systemctl status mysqld

##开机启动
systemctl enable mysqld
systemctl daemon-reload
```

### 5、修改账号密码

```shell
#1、查看MySQL为Root账号生成的临时密码
grep "A temporary password" /var/log/mysqld.log

#2、进入MySQL shell
mysql -u root -p

#3、修改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!'; #MyNewPass4!这个密码
```

### 6 、开启 MySQL 远程连接

```shell
#选择 mysql 数据库：
USE mysql;

#在 mysql 数据库的 user 表中查看当前 root 用户的相关信息：
SELECT host, user, authentication_string, plugin FROM user;

#设置root 用户远程访问：
update user set host = '%' where user ='root';

#刷新权限：
FLUSH PRIVILEGES;

#授权的所有权限
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';

#更新 root 用户密码及加密规则（如果客户端不支持加密插件）：
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'MyNewPass4!';

#刷新权限：
FLUSH PRIVILEGES;
```

### 7、新建远程用户

```shell
#1、新建远程用户
CREATE USER 'devops'@'%' IDENTIFIED BY 'MyNewPass3!';

#2、赋予指定账户指定(数据库名称.表名)远程访问权限
GRANT ALL PRIVILEGES ON mydb_name.* TO 'devops'@'%';

#3、查看权限
SHOW GRANTS FOR 'devops'@'%';

#4、收回权限
REVOKE ALL PRIVILEGES ON *.* FROM 'devops'@'%';

#5、删除用户
DROP USER 'devops'@'%';

#6、刷新权限
FLUSH PRIVILEGES;
```

### 8、 找回密码

```shell
#1.关闭MySQL
service mysql stop

#2.用以下命令启动MySQL，以不检查权限的方式启动；
service mysql start --skip-grant-tables

#3.然后用空密码方式使用root用户登录 MySQL；
mysql -u root
```

### 9.启动失败

```shell
#权限问题
chown mysql:mysql -R /var/run/mysqld

/usr/sbin/mysqld --user=mysql &
```



## Mysql卸载

### 1.查看mysql安装了哪些东西

```shell
rpm -qa |grep -i mysql
```

### 2.开始卸载

```shell
rpm -e --nodeps mysql-community-client-8.0.22-1.el7.x86_64
rpm -e --nodeps mysql80-community-release-el7-3.noarch
rpm -e --nodeps mysql-community-common-8.0.22-1.el7.x86_64
rpm -e --nodeps mysql-community-libs-8.0.22-1.el7.x86_64
rpm -e --nodeps mysql-community-server-8.0.22-1.el7.x86_64
rpm -e --nodeps mysql-community-client-plugins-8.0.22-1.el7.x86_64
rpm -e --nodeps mysql-community-libs-compat-8.0.22-1.el7.x86_64
```

或者

```yum
yum remove  mysql-community-client-8.0.22-1.el7.x86_64
yum remove  mysql80-community-release-el7-3.noarch
yum remove  mysql-community-common-8.0.22-1.el7.x86_64
yum remove  mysql-community-libs-8.0.22-1.el7.x86_64
yum remove  mysql-community-server-8.0.22-1.el7.x86_64
yum remove  mysql-community-client-plugins-8.0.22-1.el7.x86_64
yum remove  mysql-community-libs-compat-8.0.22-1.el7.x86_64
```

### 3.查看是否卸载完成

```shell
rpm -qa |grep -i mysql
```

### 4、查找mysql相关目录

```sh
find / -name mysql
```

### 5、删除相关目录

```shell
rm -rf #查找mysql相关目录
rm -rf  /usr/lib64/mysql
rm -rf  /etc/selinux/targeted/active/modules/100/mysql
rm -rf /etc/selinux/targeted/tmp/modules/100/mysql
rm -rf /var/lib/mysql
rm -rf  /var/lib/mysql/mysql
```

### 6、删除/etc/my.cnf

```shell
rm -rf /etc/my.cnf
```

### 7.删除/var/log/mysqld.log

> 如果不删除这个文件，会导致新安装的mysql无法生存新密码，导致无法登陆

```shell
rm -rf /var/log/mysqld.log
```

