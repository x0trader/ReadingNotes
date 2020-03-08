## 5.Linux软件包管理

在GNU/Linux操作系统中，RPM和DPKG是最常见的包管理工具，提供在操作系统中安装、升级、卸载需要的软件的方法，并提供对系统中所有软件状态的查询。

|包管理器|全称|操作系统|
|------|------|------|
|RPM|Redhat Package Manager|Redhat|
|DPKG|Debian Package|Debian,Ubuntu|


### 5.1 RPM包管理

RPM的常规用法是 rpm -? package.rpm,更多信息可参考 man rpm,常用参数如下：

|操作参数|释义|
|------|------|
|q|在系统中查询软件或查询指定rpm包的内容信息|
|i|在系统中安装软件|
|U|在系统中升级软件|
|e|在系统中卸载软件|
|h|用#符显示rpm安装过程|
|v|详述安装过程|
|V|校验|
|qRP|查询包的依赖关系|
|p|对RPM包进行查询，通常和其他参数同时使用|

-qlp 查询某个RPM包中的所有文件列表

-qip 查询某个RPM包的内容信息


### 5.2 DPKG包管理

一个DEB包包含了已压缩的软件文件集以及该软件的内容信息（在头文件中保存），通常文件以.deb结尾，DPKG的常规用法为 dpkg -? package.deb,更多信息参考 man dpkg,常用参数如下：

|操作参数|释义|
|------|------|
|l|在系统中查询软件内容信息|
|info|在系统中查询软件或查询指定deb包的内容信息|
|i|在系统中安装/升级软件|
|r|在系统中卸载软件，不删除配置文件|
|P|在系统中卸载软件并删除配置文件|

DEB包管理示例：

1.先查询该软件是否存在 dpkg -l pkg*

2.如果存在，可考虑删除 dpkg -P pkgxxx，或者升级 dpkg -i pkgxxx.deb

3.查询包的内容 dpkg -info pgkxxx.deb

### 5.3 YUM包管理

YUN基于RPM包管理工具，能从指定的源空间（服务器，本地目录等）自动下载目标RPM包并且安装，还可自动处理依赖性关系；还可对系统所有的软件进行升级。

YUM的RPM包来源于源空间，比如在RHEL中的/etc/yum.repos.d/.repo文件配置指定

YUM的系统配置文件位于 /etc/yum.conf

YUM的常见命令如下：

* 安装指定包 yum -y install package-name

* 升级指定包 yum update package-name

* 卸载指定包 yum remove package-name

* 列出系统中安装的软件 yum list

* 列出系统中可升级的软件 yum check-update

* 升级系统中可升级的所有软件 yum update

更多YUM的信息可参考[官网](http://fedoraproject.org/wiki/Tools/yum )

### 5.4 APT包管理

APT(Advanced Packaging Tools)最早被设计为DPKG的前端软件，现在可以通过apt-rpm支持rpm管理，APT的软件园定义位于 /etc/apt/sources.list,手动修改该文件，需要使用 sudo apt-get update来更新系统的源使新的源数据被当前系统识别。

Ubuntu中apt的配置文件位于 /ect/apt/apt.conf.d

APT常用命令

* 更新源索引 sudo apt-get update

* 安装指定软件 sudo apt-get install package-name

* 下载指定软件的源文件 sudo apt-get source package-name

* 卸载指定软件 sudo apt-get remove package-name

* 将系统所有软件升级到最新 sudo apt-get dist-upgrade

更多包工具的介绍可参考 [IBM的Linux包管理](https://www.ibm.com/developerworks/cn/linux/l-cn-rpmdpkg/index.html)

### 5.5 源代码包安装

对于下载的源代码，一般安装经过 解压缩->配置->编译->安装


### 5.6 脚本安装

对于下载的包含安装脚本的，一般安装经过 解压缩->安装