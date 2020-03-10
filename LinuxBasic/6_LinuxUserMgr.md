## 6.Linux用户管理

用户,用户组管理的相关文件如下表所示：

|配置文件|文件目录|
|------|------|
|用户信息|/etc/passwd|
|密码文件|/etc/shadow|
|用户组信息|/etc/group|
|用户组密码|/etc/gshadow|
|用户配置|/etc/login.defs,/etc/default/useradd|
|新用户信息|/etc/skel|
|登录信息|/etc/motd,/etc/issue|

### 6.1 用户管理

Linux用户分为三类：

* 超级用户 root,UID=0

* 普通用户 UID 500-60000

* 伪用户 UID 1-499

其中 伪用户 通常不需要登录或者无法登录，可以没有宿主目录。

一般是与系统和程序服务相关,比如 bin,daemon,shutdown,halt.任何Linux系统默认都有这些伪用户

还有一些与Linux系统的进程相关，比如 mail,news,games,apache,ftp,mysql,sshd等
用户管理的相关文件如下表所示：


#### **/etc/passwd 文件格式**

|字段|含义|
|------|------|
|用户名|用户登录系统使用的用户名|
|密码|密码位|
|UID|用户标识号|
|GID|缺省组标志号|
|注释性描述|例如存放用户全名等信息|
|宿主目录|用户登录系统后的缺省目录|
|命令解释器|用户使用的shell,默认为bash|

####  **/etc/shadow 文件格式**

|字段|含义|
|------|------|
|用户名|用户登录系统使用的用户名|
|密码|加密密码|
|最后一次修改时间|用户最后一次修改密码的天数|
|最小时间间隔|两次修改密码之间的最小天数|
|最大时间间隔|密码保持有效的最多天数|
|警告时间|从系统开始警告到密码失效的天数|
|账号闲置时间||
|失效时间|密码失效的绝对天数|
|标志|一般不使用|

#### 常用用户操作

* 手工添加用户

1. 分别在 /etc/passwd,/etc/shadow添加记录

2. 创建用户宿主目录

3. 在用户宿主目录设置默认的配置文件

4. 设置用户初始密码

* 命令添加用户

1. useradd 设置选项 用户名 

|参数|含义|
|------|------|
|u|UID|
|g|缺省所属用户组GID|
|G|指定用户所属多个组|
|d|宿主目录|
|s|命令解释器|
|c|描述信息|
|e|指定用户失效时间|

2. passwd sam


* 修改用户信息 usermod

> usermod -G softgroup sam 将用户sam添加到用户组softgroup中

> usermod -l sam -d /home/sam -g lampbrother liming 修改 liming->sam,加入到组lampbrother,用户目录变为/home/sam

* 删除用户 userdel -r 用户名 （-r删除用户目录）

* 禁用用户 usermod -L sam, passwd -l sam

* 恢复用户 usermod -U sam, passwd -u sam
* 检测/etc/passwd文件 pwck

* 编辑/etc/passwd文件 vipw

* 查看用户id和组信息 id

* 查看用户详细信息 finger

* 切换用户 su

* 查看用户密码状态 passwd -S

* 查看当前登录用户信息 who w

### 6.2 用户组管理

每个用户都至少属于一个用户组，每个用户组可以包括多个用户，同一用户组的用户享有该组共有的权限。

####  **/etc/group 文件格式**

|字段|含义|
|------|------|
|组名|用户登录时所在组|
|组密码|一般不使用|
|GID|组标识号|
|组内用户列表|属于该组的所有用户列表|


####  **/etc/gshadow 文件格式**

|字段|含义|
|------|------|


#### 常用用户组操作

* 添加用户组 groupadd

> groupadd -g 888 webadmin

* 删除用户组 groupdel

> groupdel webadmin

* 修改用户组信息 groupmod

> groupmod -n apache webadmin  webadmin->apache

* 设置组密码及管理组内成员 gpasswd

* 查看用户隶属于哪些用户组 groups

* 切换用户组 newgrp

* 用户组配置文件检测 grpck

* 修改文件所述组 chgrp

* 编辑/etc/group vigr
