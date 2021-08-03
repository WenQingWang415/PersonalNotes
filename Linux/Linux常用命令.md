### Linux系统的文件结构

> 登录系统之后，在当前命令窗口输入命令
>
> ```bash
>  ls /
> ```
>
> 如图：
>
> ![image.png]( https://wwq-notes.oss-cn-guangzhou.aliyuncs.com/35SZ6eBfHNpF8Qy.png)
>
> 目录结构的解释：
>
> [菜鸟教程目录结构解释](https://www.runoob.com/linux/linux-system-contents.html)

### 目录操作

#### 切换目录（cd）

> ```shell
> cd /              #切换到根目录
> cd /bin           #切换到跟目录的斌目录
> cd ../            #返回上一级目录或者  cd ..
> cd ~              #切换到home目录   注意看目录解释：每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的
> cd -              #切换到上次访问目录
> cd xx(文件名)      #每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的
> cd /xxx/xx/x      #可以输入完整的路径，直接切换到目标目录，输入过程中可以使用tab键快速补全
> ```

#### 查看目录（ls）

> ```shell
> ls /             #查看所有目录
> ls -a            #查看当前目录下所有的目录和文件（包括隐藏目录）
> ls /bin          #查看指定目录下的所有文件和目录
> ```
>
> ```shell
> ls -l            #列表查看当前目录下的所有文件和目录（列表查看，显示更多信息）与命令`ll`一样
>                  #显示一个文件的属性以及文件所属的用户和组
> ```
>
> 结果如下：
>
> ```shell
> [root@iZkq4tb7g6gh8mZ /]# ls -l
> total 64
> lrwxrwxrwx.  1 root root     7 Nov 20 16:24 bin -> usr/bin
> dr-xr-xr-x.  5 root root  4096 Nov 20 16:36 boot
> drwxr-xr-x  19 root root  2960 Dec 22 16:42 dev
> drwxr-xr-x. 76 root root  4096 Dec 22 16:42 etc
> 
> ```
>
> 实例中，bin文件的第一个属性用`d`表示。`d`在Linux中代表该文件是一个目录文件
>
> - 当为`d`则是目录
> - 当为`-`则是文件
> - 若是`l`则表示链接文档（link file）
> - 若是`b`则表示为装置文件里面的可供储存的接口设备(可随机存取装置)；
> - 若是`c`则表示装置文件里面的串行端口设备，列如：键盘，鼠标
>
> 接下来的字符中，以三个一组，且均为`rwx`的三个参数的组合，其中`r`代表可读(read),`w`代表可写(write),`x`代表可执行（exexute）.
>
> 这三个权限的位置不会变，如果没有权限，就会出现减号`-`而已
>
> 每个文件的属性由左边第一部分的 10 个字符来确定（如下图）。
>
> ![363003_1227493859FdXT](https://www.runoob.com/wp-content/uploads/2014/06/363003_1227493859FdXT.png)
>
> 第 **0** 位确定文件类型，第 **1-3** 位确定属主（该文件的所有者）拥有该文件的权限。
>
> 第4-6位确定属组（所有者的同组用户）拥有该文件的权限，第7-9位确定其他用户拥有该文件的权限。
>
> 其中，第 **1、4、7** 位表示读权限，如果用 **r** 字符表示，则有读权限，如果用 **-** 字符表示，则没有读权限；
>
> 第 **2、5、8** 位表示写权限，如果用 **w** 字符表示，则有写权限，如果用 **-** 字符表示没有写权限；
>
> 第 **3、6、9** 位表示可执行权限，如果用 **x** 字符表示，则有执行权限，如果用 **-** 字符表示，则没有执行权限。

#### chgrp：更改文件属组

语法：

```shell
chgrp [-R] 属组名 文件名
```

参数选项

- -R：递归更改文件属组，就是在更改某个目录文件的属组时，如果加上-R的参数，那么该目录下的所有文件的属组都会更改。

#### chown：更改文件属主，也可以同时更改文件属组

语法：

```shell
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名
```



#### chmod：更改文件9个属性

> linux文件属性设置的方法，一种数字（<span style="color:red">常用</span>），一种符号
>
> Linux 文件的基本权限就有九个，分别是 **owner/group/others(拥有者/组/其他)** 三种身份各有自己的 **read/write/execute** 权限。
>
> 先复习一下刚刚上面提到的数据：文件的权限字符为： **-rwxrwxrwx** ， 这九个权限是三个三个一组的！其中，我们可以使用数字来代表各个权限，各权限的分数对照表如下：
>
> - r:4
> - w:2
> - x:1
>
> 每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的，例如当权限为： **-rwxrwx---** 分数则是：
>
> - owner = rwx = 4+2+1 = 7
> - group = rwx = 4+2+1 = 7
> - others= --- = 0+0+0 = 0
>
> 所以等一下我们设定权限的变更时，该文件的权限数字就是 **770**。变更权限的指令 chmod 的语法是这样的：
>
> ```shell
> chmod 770 文件或者目录
> ```
>
> ![image.png]( https://wwq-notes.oss-cn-guangzhou.aliyuncs.com/fZcxCQeXnBb29zW.png)

#### 创建目录（mkdir）

```shell
mkdir test                      #在当前目录下创建一个test目录
mkdir /WenQIngWang/test         #在指定的目录下创建test目录
mkdir -p /test1/test2/test3     #创建多层目录
mkdir -m 777 test2              #创建权限目录，
```

#### 删除目录和文件（rm）

==这个 rmdir 仅能删除空的目录，你可以使用 rm 命令来删除非空目录==

```shell
rm 文件名              #删除当前目录下的文件
rm -f 文件名           #删除当前目录的的文件（不询问）
rm -r 文件夹名         #递归删除当前目录下此名的目录
rm -rf 文件夹名        #递归删除当前目录下此名的目录（不询问）
rm -rf *              #将当前目录下的所有目录和文件全部删除
rm -rf /*             #将根目录下的所有文件全部删除【慎用！相当于格式化系统】
rmdir  目录名          #删除目录
rmdir -p 目录名        #利用 -p 这个选项，立刻就可以将 test1/test2/test3/test4 依次删除。
```

#### 修改目录（mv）

```shell
mv 当前目录名 新目录名         #修改目录名，同样适用与文件操作
mv /usr/tmp/tool /opt       #将/usr/tmp目录下的tool目录剪切到 /opt目录下面
mv -r /usr/tmp/tool /opt    #递归剪切目录中所有文件和文件夹
```

#### 拷贝目录(cp)

```shell
cp 来源文件 目标   #[-adfilprsu] 来源档(source) 目标档(destination)
```

#### 查看当前目录（pwd）

```shell
pwd
```

### 文件操作

#### 新增文件(touch)

```shell
touch a.text  #在当前目录下创建名为a的txt文件（文件不存在），如果文件存在，将文件时间属性修改为当前系统时间
```

#### 文件内容查看

##### cat 

> 由第一行开始显示文件内容
>
> ```shell
> cat  [-AbEnTv] 文件名
> ```
>
> 选项和参数
>
> - -A ：相当於 -vET 的整合选项，可列出一些特殊字符而不是空白而已；
> - -b ：列出行号，仅针对非空白行做行号显示，空白行不标行号！
> - -E ：将结尾的断行字节 $ 显示出来；
> - -n ：列印出行号，连同空白行也会有行号，与 -b 的选项不同；
> - -T ：将 [tab] 按键以 ^I 显示出来；
> - -v ：列出一些看不出来的特殊字符

##### tac

> 与cat命令相反，文件内容从最后一行开始显示
>
> ```shell
> tac 文件
> ```

##### nl

> 显示行号
>
> ```shell
> nl [-bnw]  文件
> ```
>
> 选项和参数
>
> - -b ：指定行号指定的方式，主要有两种：
>   -b a ：表示不论是否为空行，也同样列出行号(类似 cat -n)；
>   -b t ：如果有空行，空的那一行不要列出行号(默认值)；
> - -n ：列出行号表示的方法，主要有三种：
>   -n ln ：行号在荧幕的最左方显示；
>   -n rn ：行号在自己栏位的最右方显示，且不加 0 ；
>   -n rz ：行号在自己栏位的最右方显示，且加 0 ；
> - -w ：行号栏位的占用的位数。

##### more 

> 一页一页翻动
>
> ```shell
> more 文件
> ```
>
> 在 more 这个程序的运行过程中，你有几个按键可以按的：
>
> - 空白键 (space)：代表向下翻一页；
> - Enter     ：代表向下翻『一行』；
> - /字串     ：代表在这个显示的内容当中，向下搜寻『字串』这个关键字；
> - :f      ：立刻显示出档名以及目前显示的行数；
> - q       ：代表立刻离开 more ，不再显示该文件内容。
> - b 或 [ctrl]-b ：代表往回翻页，不过这动作只对文件有用，对管线无用。

##### less

> 一页一页翻动
>
> ```shell
> lass 文件
> ```
>
> less运行时可以输入的命令有：
>
> - 空白键  ：向下翻动一页；
> - [pagedown]：向下翻动一页；
> - [pageup] ：向上翻动一页；
> - /字串   ：向下搜寻『字串』的功能；
> - ?字串   ：向上搜寻『字串』的功能；
> - n     ：重复前一个搜寻 (与 / 或 ? 有关！)
> - N     ：反向的重复前一个搜寻 (与 / 或 ? 有关！)
> - q     ：离开 less 这个程序；

##### head

> 取出文件前面几行
>
> ```shell
> head [-n number] 文件 
> ```
>
> 选项与参数：
>
> - -n ：后面接数字，代表显示几行的意思
>
> ```sh
> [root@www ~]# head /etc/man.config
> ```
>
> 默认的情况中，显示前面 10 行！若要显示前 20 行，就得要这样：
>
> ```shell
> [root@www ~]# head -n 20 /etc/man.config
> ```

##### tail

> 取出文件后面几行
>
> 语法：
>
> ```shell
> tail [-n number] 文件 
> ```
>
> 选项与参数：
>
> - -n ：后面接数字，代表显示几行的意思
> - -f ：表示持续侦测后面所接的档名，要等到按下[ctrl]-c才会结束tail的侦测
>
> ```shell
> [root@www ~]# tail /etc/man.config
> # 默认的情况中，显示最后的十行！若要显示最后的 20 行，就得要这样：
> [root@www ~]# tail -n 20 /etc/man.config
> ```

#### 编辑文件(vi)

```shell
  vi 文件名              //打开需要编辑的文件
  --进入后，操作界面有三种模式：命令模式（command mode）、插入模式（Insert mode）和底行模式（last line mode）
  命令模式
  -刚进入文件就是命令模式，通过方向键控制光标位置，
  -使用命令"dd"删除当前整行
  -使用命令"/字段"进行查找
  -按"i"在光标所在字符前开始插入
  -按"a"在光标所在字符后开始插入
  -按"o"在光标所在行的下面另起一新行插入
  -按"："进入底行模式
  插入模式
  -此时可以对文件内容进行编辑，左下角会显示 "-- 插入 --""
  -按"ESC"进入底行模式
  底行模式
  -退出编辑：      :q
  -强制退出：      :q!
  -保存并退出：    :wq
  ## 操作步骤示例 ##
  1.保存文件：按"ESC" -> 输入":" -> 输入"wq",回车     //保存并退出编辑
  2.取消操作：按"ESC" -> 输入":" -> 输入"q!",回车     //撤销本次修改并退出编辑
  ## 补充 ##
  vim +10 filename.txt                   //打开文件并跳到第10行
  vim -R /etc/passwd                     //以只读模式打开文件
```

### Linux链接

> Linux链接分为两种：硬链接，软链接
>
> ​	硬链接：A→B,假设B是A的硬链接，那么他们两个指向同一个文件，一个文件允许有多个路径，用户可以通过这种机制建立硬链接到一些重要文件，防止误删
>
> ​    软链接：类似windows的快捷键，删除源文件，快捷方式也访问不了
>
> ```shell
> [root@iZkq4tb7g6gh8mZ WenQingWang]# touch wen             #创建文件
> [root@iZkq4tb7g6gh8mZ WenQingWang]# ln wen wenqing        #创建wen的硬链接wenqing
> [root@iZkq4tb7g6gh8mZ WenQingWang]# ln -s wen wenqing1    #创建wen的软链接 wenqing1
> [root@iZkq4tb7g6gh8mZ WenQingWang]# ll                    #查看 显示的文件
> total 28
> drwxr-xr-x 2 root root  4096 Dec 23 16:05 test2
> -rw-r--r-- 1 root root 23150 Dec 23 15:51 test.text
> -rw-r--r-- 2 root root     0 Dec 23 17:23 wen
> -rw-r--r-- 2 root root     0 Dec 23 17:23 wenqing
> lrwxrwxrwx 1 root root     3 Dec 23 17:24 wenqing1 -> wen   #lrwxrwxrwx l表示链接文档 -表示文件 d表示目录
> ```
>
> ```shell
> [root@iZkq4tb7g6gh8mZ WenQingWang]# echo wenqingwang >>wen  #ccho "添加字符"文件
> [root@iZkq4tb7g6gh8mZ WenQingWang]# cat wen                 #查看文件 wen输出
> wenqingwang
> [root@iZkq4tb7g6gh8mZ WenQingWang]# cat wenqing             #查看文件 wenqing输出
> wenqingwang
> [root@iZkq4tb7g6gh8mZ WenQingWang]# cat wenqing1            #查看文件wneqing1输出
> wenqingwang
> [root@iZkq4tb7g6gh8mZ WenQingWang]# rm wen                  #删除文件 wen
> rm: remove regular file ‘wen’? y
> [root@iZkq4tb7g6gh8mZ WenQingWang]# cat wenqing1            #对软链接有影响，提示找不到
> cat: wenqing1: No such file or directory
> [root@iZkq4tb7g6gh8mZ WenQingWang]# cat wenqing            #对硬链接没有影响
> wenqingwang
> ```
>
> 总结：
>
> 删除软链接的目标文件，对 软链接找不到文件
>
> 删除硬链接的目标文件 ，对硬链接木影响