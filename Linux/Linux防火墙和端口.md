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
开端口命令：firewall-cmd --zone=public --add-port=8091/tcp --permanent
重启防火墙：systemctl restart firewalld.service
#关闭端口
关闭端口命令： firewall-cmd --permanent --zone=public --remove-port=8091/tcp
重启防火墙：systemctl restart firewalld.service
--zone #作用域
--add-port=80/tcp  #添加端口，格式为：端口/通讯协议
--permanent   #永久生效，没有此参数重启后失效
```

