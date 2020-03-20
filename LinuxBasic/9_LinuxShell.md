## 9.Linux Shell编程

### 9.1 Shell概述

只有kernel能直接控制硬件，图形界面和命令行只是用户和kernel之间的桥梁，在Linux下，命令行程序叫做shell，它有如下作用：

* 解释用户输入的命令，传递给kernel

* 调用其他程序，给其他程序传给数据或参数，并获取程序的处理结果

* 在多个程序之间传递数据，把一个程序的输出作为另一个程序的输入

Shell是一种脚本语言，第一行 #!/bin/bash 标志该Shell脚本由哪个shell解释

一般shell的编写流程：

1. 编写 shell 脚本 （vi hi.sh）

2. 赋予可执行权限 （chmod a+x hi.sh）

3. 执行，调试 （./hi.sh）

### 9.2 Shell相关语法

#### 变量

在bash shell 中，每一个变量的值都是字符串，也可使用 declare显示定义变量的类型

shell定义变量的方式

> var1=value1 (如果value1包含空格，必须用引号括起来)

> val1="value1"

> val1='value1'

变量命名规范：

* 变量名由 数字，字母，下划线组成

* 必须以字母或者下划线开头

* 不能使用shell里的关键字


变量类型：

* 局部变量：在脚本或命令中定义，仅在当前脚本有效

* 环境变量： 所有程序，包括shell启动的程序都能访问环境变量

* shell变量： 由shell程序设置的特殊变量，有一部分是环境变量，有一部分是局部变量

#### 关键字

|关键字|含义|
|------|------|
|echo|打印文字到屏幕|
|exec|执行另一个shell脚本|
|read|读标准输入|
|expr|对整数型变量进行算术运算|
|test|用于测试变量是否相等，是否为空，文件类型等|
|exit|退出|
