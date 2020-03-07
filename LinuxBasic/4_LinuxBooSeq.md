## 4.Linux引导流程解析

### 4.1 Linux引导流程

'''flow

st=start: 固件firmware(CMOS/BIOS)

ed=end: 读取执行配置文件/etc/inittab

op1=operation: 自举程序BootLoader(GRUB)

op2=operation: 载入内核 Kernel

op3=operation: 启动进程 init

'''

### 4.2 Linux运行级别

### 4.3 Linux启动服务管理



### 4.4 GRUB配置与应用

GRUB的配置文件默认为/boot/grub/grub.confg

ls -l /boot/grub/grub.conf，对应配置文件的配置项解释如下

|项目|释义|
|------|------|
|default|缺省启动系统|
|timeout|缺省等待时间|
|splashimage|GRUB界面图片|
|hiddenmenu|隐藏菜单|
|title|菜单项名称|
|root|设置GRUB的根设备所在的分区|
|kernel|内核文件所在位置|
|initrd|加载镜像文件|


GRUB命令如下：

|功能键|释义|
|------|------|
|e|编辑当前的启动菜单项|
|c|进入GRUB的命令行方式|
|b|启动当前的菜单项|
|d|删除当前行|
|ESC|返回GRUB启动菜单界面，取消对当前菜单项所作的任何改动|


### 4.5 启动故障分析与解决


* GRUB修复
开机后进入grub界面没有菜单，只有grub>提示符，解决方案

'''
cat /grub/grub.conf

root (dh0,6)

kernel (hd0,6) /vmlinuz-2.6.18-14 root=LABEL=/

initrd (hd0,6) /initrd-2.6.18-14.img

boot
'''

* Linux修复模式

安装盘放到光驱，重新启动机器，在BIOS中把系统设置为光驱引导

安装界面出现后，F5 进入 Linux rescue模式说明

在boot提示符下 输入 linux rescue,回车进入 修复模式

更多参考 [进入Linux救援（rescue）模式的四大法门](https://blog.csdn.net/zhubinqiang/article/details/38331417)