### 查看端口，结束端口

> ```shell
> #安装 lsof
>  yum install lsof
> #查看那个进程占用了7070端口 
> lsof -i:7070 
> // 杀掉进程6610  pId
> kill -s 9 6610
> ```
>
> 