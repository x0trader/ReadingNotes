## 2.Linux常用命令

Linux文件命名规则如下：

1) 除了/，其余字符都合法,/表示根目录
2) 空格，制表符以及特殊字符最好不用
3) 避免使用.作为普通文件开头
4) 文件名 大小写敏感

命令的格式如下：

命令 -选项 参数

如 ls -d /etc

其中多个选项，可以放在一起


**.**代表当前目录 

**..**代表当前目录的父目录

### 2.1 文件处理命令

* ls   list,显示目录文件

* cd change directory,切换目录

* pwd print working directory,打印当前所在的工作目录

* touch 创建空文件

* mkdir make directories 创建新目录

* cp copy，复制文件或者目录

> cp 源文件 目标目录

>cp -R 源目录 目标目录

* mv move 移动文件,更名

> mv file1 dir1

> mv file1 file2

* rm remove 删除文件/目录

> rm file1

> rm -r dir1

* cat concateenate and display files,显示文件内容

* more 分页显示文件内容

> 空格/f 显示下一页

> Enter 显示下一行

> q/Q 退出

* head 查看文件的前几行

> head -20 /etc/services

* tail 查看文件的后几行

* ln link,产生链接文件

> ln -s /etc/issue  /issue.soft

> ln /etc/issue /issue.hard


### 2.2 权限管理命令

* chmod change the permissions mode of a file,改变文件或者目录权限


* chown change file ownership,改变文件或目录的所有者

* chgrp change file group ownership,改变文件或目录的所属组

* umask 显示、设置文件的缺省权限


### 2.3 文件搜索命令

* which 显示系统命令所在路径

> which ls

* find 查找文件或目录

> find /etc *a*.txt



### 2.4 帮助命令

* man manual 获得帮助信息

> man ls

* info information，获得帮助信息

> info ls

* wathis/apropos/makewathis 获得索引的简短说明信息

> whatis ls
### 2.5 压缩解压缩命令


### 2.6 网络通信命令


### 2.7 系统关机命令



