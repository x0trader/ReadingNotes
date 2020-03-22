## 9.Linux Shell编程

### 9.1 Shell概述

只有kernel能直接控制硬件，图形界面和命令行只是用户和kernel之间的桥梁，在Linux下，命令行程序叫做shell，它有如下作用：

* 解释用户输入的命令，传递给kernel

* 调用其他程序，给其他程序传给数据或参数，并获取程序的处理结果

* 在多个程序之间传递数据，把一个程序的输出作为另一个程序的输入

Shell是一种脚本语言，第一行 #!/bin/bash 标志该Shell脚本由哪个shell解释

一般shell的编写流程：

1. 编写 shell 脚本 （vi hi.sh）

2. 赋予可执行权限 （chmod a/u+x hi.sh）

3. 执行，调试 （./hi.sh）

Shell的结构如下：

1. #! 指定执行脚本的shell

2. \#注释行

3. 命令和控制结构

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

变量使用：

使用一个已定义的变量，前面加 $ 即可

> url="wwww.hao123.com"

> echo $url

> echo ${url} 

变量外的{}可选，是为了帮助解释器识别变量边界，比如

> echo "Please vist this website $urlddd"

>output: Please vist this website $urlddd

修改变量的值：

> url="cn.bing.com"

* **''** 和 **""**的区别（单引号和双引号的区别）

'' 包围变量时，''里面是什么就输出什么，即使里面有命令或者变量

"" 包围变量时，输出时会先解析里面的变量和命令

将命令的值赋值给变量：

> var1=$(command)

> var1=`command` (反引号 容易 与 单引号 混淆，建议使用 $(command)的形式)

删除变量

> unset var1

变量类型：

* 局部变量：在脚本或命令中定义，仅在当前脚本有效

* 环境变量： 所有程序，包括shell启动的程序都能访问环境变量

* shell变量： 由shell程序设置的特殊变量，有一部分是环境变量，有一部分是局部变量

常见的特殊变量如下表：

|特殊变量|含义|
|------|------|
|$n|文件的第n个参数,$0 程序单位文件名|
|$*|程序的所有参数|
|$#|程序的参数个数|
|$$|程序的PID|
|$!|执行上一个后台命令的PID|
|$?|执行上一个命令的返回值|


#### 关键字

|关键字|含义|用法|
|------|------|------|
|echo|打印文字到屏幕||
|exec|执行另一个shell脚本||
|read|读标准输入，赋值给变量|read username|
|expr|对整数型变量进行算术运算|expr 3+5, 'expr $a + $b / $c'|
|test|用于测试变量是否相等，是否为空，文件类型等|test str1=str2,test str2 |
|exit|退出|exit 0|

字符串测试

|用法|含义|
|------|------|
|test str1=str2|测试字符串是否相等|
|test str1!=str4|测试字符串是否不等|
|test str1|测试字符串是否不为空|
|test -n str1|测试字符串是否不为空|
|test -z str1|测试字符串是否为空|

整数测试

|用法|含义|
|------|------|
|test int1 -eq int2|测试整数是否相等|
|test int1 -ge int2|测试int1>=int2|
|test int1 -gt int2|测试int1>int2|
|test int1 -le int2|测试int1<=int2|
|test int1 -lt int2|测试int1 < int2|
|test int1 -ne int2|测试int1 != int2|

文件测试

|用法|含义|
|------|------|
|test -d file|文件是否为目录|
|test -f file|文件是否常规文件|
|test -x file|文件是否可执行|
|test -r file|文件是否可读|
|test -w file|文件是否可写|
|test -a file|文件是否存在|
|test -s file|文件大小是否非0|

变脸测试语句一般作为if语句的测试条件，如：

    if test -d $a then
        echo $a
    fi    

变量测试语句可用[]进行简化，

    if [-d $a]; then
        echo $a
    fi

#### 流控制语句

**if/else**

    if cond1 -a/-o cond2 then
        command1
    elif cond3 then
        command2
    else
        command3
    fi
  

**case/esac**

    echo "input a number in [1-3]"
    read num
    case $num in
    1)
        echo "select 1"
        ;;
    2)
        echo "select 2"
        ;;
    3)
        echo "select 3"
        ;;
    esca

**for/done**

    for var1 in vartable
    do
        command_n
    done

    for Day in Sunday Saturday
    do
        echo "$Day is holiday"
    done      

  

**while/do**

    counter=0
    while [$counter -lt 5]
    do
        counter="expr $counter+1"
        echo $counter
    done

  

**until/do**

    counter=0
    until [$counter -lt 5]
    do
        echo $counter
        counter="expr $counter+1"
    done

可以使用break continue跳出循环或者继续下一次循环


#### 函数

函数模板如下：

    function function_name(){
        list of commands
        [return value]
    }

样例：

    #!/bin/bash

    #Define function
    Hello(){
        echo "This is Hello function"
    }

    Hello
    
### 9.3 Shell脚本调试    

|调试命令|释义|
|------|------|
|sh -x script1|执行脚本并显示所有变量的值|
|sh -n script1|不执行，仅检查语法，返回所有的语法错误|
