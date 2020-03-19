## 8.Linux文件系统管理

### 8.1 文件系统构成及命令

#### 文件系统构成


|目录|含义|
|------|------|
|/usr/bin,/bin|存放所有用户可以执行的命令|
|/usr/sbin,/sbin|存放只有root能执行的命令|
|/home|用户缺省宿主目录|
|/proc|虚拟文件系统，存放当前进程信息|
|/dev|存放设备文件|
|/lib|存放系统程序运行所需的共享库|
|/lost+found|存放系统出错的检查结果|
|/tmp|存放临时文件|
|/etc|系统配置文件|
|/var|包含经常变动的文件，如邮件，日志文件、计划任务等|
|/usr|存放所有命令、库、手册页等|
|/boot|内核文件及自举程序文件保存位置|
|/mnt|临时文件系统的安装点|
|/var|包含经常变动的文件，如邮件，日志文件、计划任务等|


#### 常见命令

常用文件系统相关命令如下表：

|命令|含义|
|------|------|
|df|查看分区使用情况|
|du|查看文件、目录大小|
|stat|查看文件详细时间参数|
|md5sum|校验文件MD5值|
|fsck,e2fsck|检测修复文件系统|

### 8.2 硬盘分区及管理

#### 添加硬盘分区

1. 划分分区 fdisk

2. 创建文件系统 mkfs

3. 尝试挂载 mount

4. 写入配置文件 /etc/fstab


### 8.3 磁盘配额

1. 开启分区配额功能

编辑 /etc/fstab 文件，在挂载属性上加上标志 **usrquota**或者**grpquota**

2. 建立配额数据库

3. 启动配额功能

4. 编辑用户配额


### 8.4 备份与恢复


#### 备份的原因

因为系统存在以下潜在风险：
* 系统硬件故障

* 软件故障

* 电源故障

* 用户的误操作

* 人为破坏

* 缓存中的内容没有及时地写入磁盘

* 自然灾害

#### 备份的介质

从 可靠性，速度，价格之间进行权衡


#### 备份策略

* 完全备份

每隔一段时间对系统进行一次完全的备份

* 增量备份

首先进行完全备份，然后每隔一段时间进行增量备份


#### 备份的分类

* 系统备份

实现对操作系统和应用程序的备份

尽量在系统崩溃之后能快速简单完全的恢复系统

主要备份 /etc,/boot,/var/log,/usr/log 等

一般只有当系统内容发生变化时才进行

* 用户备份

实现对用户文件的备份 /home

用户的数据变动频繁

通常采用增量备份策略进行

#### 备份命令

> cp -Rpu 备份目录 目标目录 (p 保持备份目录及文件属性， -u 增量备份)

远程备份用 scp

tar 命令举例

> tar -zcf /backup/sys_20200303.tar.gz /etc /boot 备份多个目录

> tar -zxf /backup/sys_20200303.tar.gz 还原

> tar -zxf /backup/sys_20200303.tar.gz etc/group 只恢复备份中指定目录

> tar -rf /backup/sys_20200303.tar.gz /etc/default/useradd 将/etc/default/useradd 追加
