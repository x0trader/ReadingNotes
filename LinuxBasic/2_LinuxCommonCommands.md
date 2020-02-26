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

\. 代表当前目录 

\.\. 代表当前目录的父目录

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

> u User,文件或目录的拥有者

> g Group,文件或目录的所属群组

> o Other,除文件或目录拥有者和所属群组之外的

> a All,全部用户

> r 读取权限, = 4

> w 写入权限, = 2

> x 执行权限, = 1

> *-* 不具任何权限,=0

> chmod a+x file1 对file1的u g o 设置为可执行权限

> chmod u+w,g+x,o-w file1  对file1设置为u 可写，g可执行，o 可读权限

> chmod 764 file1 对file1设置为 u 全部操作,g 可读写,o 可读

* **chown** change file ownership,改变文件或目录的所有者

* **chgrp** change file group ownership,改变文件或目录的所属组

> chgrp -R mengxin /usr/mengxin 将/usr/mengxin及其下子目录所有的文件的用户组改为 mengxin

> cat /etc/group 查看所有的组信息


* umask 显示、设置文件的缺省权限

> umask -S 显示新建目录或者 目录缺省的 rwx形式的权限

> umask u=,g=w,o=rwx 对于创建的新文件，其u的权限为改变，g的没了w/写 权限，o 的没了任何权限。  在= 操作符上，chmod利用它来设置指定的权限，umask利用它来在原来的权限基础上删除指定的权限


### 2.3 文件搜索命令

* which 显示系统命令所在路径

> which ls

* find [选项] 参数  查找文件或目录

> find /etc -name \*a.txt 查找 /etc目录下 名字 符合 *a.txt的文件  【根据文件或正则表达式进行匹配】

> find . -name "\*.txt" -o -name "\*.pdf"

> find . ! -name "\*.txt" 找出当前目录及子目录下 不为*.txt的文件【否定词参数】

> find . -type [参数类型 f 普通文件  l 符号连接   d 目录   c 字符设备   b 块设备   s 套接字   p Fifo] 根据文件类型进行搜索

* **locate**  list files in database,寻找文件或目录

> locate file1 列出跟file1相关的文件


* **updatedb** update the slocate database，建立整个系统目录文件的数据库  (root权限)

* **grep** 在文件中搜索字符匹配的行并输出

> grep ftp /etc/services 

### 2.4 帮助命令

* **man** manual 获得帮助信息

> man ls

* **info** information，获得帮助信息

> info ls

* **whatis/apropos/makewhatis** 获得索引的简短说明信息

> whatis ls

> makewhatis 建立whatis apropos搜索使用的数据库，如果使用whatis apropos发生错误，则是whatis database没建立好

### 2.5 压缩解压缩命令

* **gzip** GNU zip 压缩文件

> gzip \* 把当前目录下的每个文件压缩成.gz文件

> gzip -l \* 详细显示当前目录下每个压缩的文件信息


* **gunzip** GNU unzip 解压缩.gz的压缩文件,实为gzip的硬连接

> gunzip file1.gz  等同 gzip -d file.gz

* **tar** 压缩解压命令 打包目录   tar \[选项\] 目录

> 选项 -c 产生.tar压缩文件, -v 显示详细信息, -f 指定压缩后的文件名, -z 打包同时压缩

> tar -zcvf a.tar dir1 将目录dir1压缩成一个打包并压缩的文件

> tar -zxvf dir1.tar.gz

* **zip** 压缩文件或目录

> zip services.zip /etc/services  压缩文件

> zip -r test.zip /test 压缩目录

* **unzip** 解压缩文件

> unzip test.zip

* **bzip2** 压缩文件

> bzip2 -k file1 产生压缩文件后保留原文件

> bzip2 file1 产生压缩文件后不保留原文件

* **bunzip2** 解压缩文件

> bunzip2 \[-k\] file1.bz2


### 2.6 网络通信命令

* **write** 向另外一个用户发信息，以Ctrl+D结束

> write Jane

* **wall** 向所有用户广播信息

> wall Happy New Year!

* **ping** 测试网络连通性

> ping 192.168.1.1

* **ipconfig** 查看网络设置信息

> ipconfig -a

### 2.7 系统关机命令

* **shutdonw** 关机 (root)

> sudo shutdown -h now

* **reboot** 重启系统


### 2.8 bash应用技巧

* 命令别名

> alias copy=cp , alias xrm="rm -r"

> alias 查看别名信息

> unalias copy 删除别名


* 输入输出重定向

> ls -l /tmp > /tmp.msg  >/>> 输出重定向

> wall < /etc/motd   < 输入重定向

> cp -R /usr /backup/usr.bak 2> /bak.error  2> 错误输出重定向

* 管道

> cmd1|cmd2 将cmd1的输出传给cmd2的输入

> ls -l /etc|more

> ls -l /etc|grep init

* 命令连接符

>;  间隔的命令按顺序依次执行

>&& 前后命令执行存在逻辑与关系，后一个的命令执行依赖于前一个命令执行成功

>|| 前后命令存在逻辑或关系，后一个命令执行依赖于前一个命令执行失败


* 命令替换符

> ls -l "which touch" 将一个参数的输出作为另一个命令的参数


