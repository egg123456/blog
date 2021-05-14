---
title: shell
date: 2018/5/14
categories:
- OS
---
> Shell 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。Shell 脚本（shell script），是一种为 shell 编写的脚本程序。

# echo
read name       # 标准输入赋值给name
echo $name      # 输出 name的值
echo -e "\n 换行"   # 开启转义 \n 换行
echo "It is a test" > myfile        # 输出定向到文件 如若文件存在且有内容 则重写文件
echo `date`         # 反引号date输出时间

# variable
## defined
```bash
your_number=1
your_single_quotation_mark='egg'     # 单引号内的变量无用
your_double_quotation_mark="egg"
your_array=(value0 value1 value2 value3) # 以空格隔开
```
tips: 变量名、值和等号之间不能有空格 使用时 example; ${var} 或 $var

## variable operation
```bash
echo `expr index "$string_concat" e`  # 字符所在位置从1开始没有为0
echo $string_concat ${#string_concat} ${string_concat:2:4}  # 字符串长度 从字符串第2个字符开始截取4个字符
echo ${array[1]} ${#array} ${array[@]}  # 数组第二个值 数据组长度 所有数组值
```

## type
+ 局部变量 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
+ 环境变量 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
+ shell变量 shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

# shell 传参
```bash
echo "脚本参数 执行 sh ./learn.sh a 100 c"
echo "执行的文件名：$0";                # 执行的文件名即sh 命令之后的文件和路径 ./learn.sh
echo "第一个参数为：$1";                # a
echo "第二个参数为：$2";                # 100
echo "第三个参数为：$3";                # c
echo "参数个数为：$#";                  # 3
echo "传递的参数作为一个字符串显示：$*";    # a 100 c 
echo "脚本运行的当前进程ID号 $$"            # 4904
echo "后台运行的最后一个进程的ID号 $!"
echo "显示Shell使用的当前选项，与set命令功能相同 $-"    # hB
echo "显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误 $?"   # 0
```

# 原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。
```bash
a=10;b=20
echo "a + b : `expr $a + $b` `expr $a \* $b`"       # 30 200
```

# 流程控制
```bash
a=10
b=20
if [ $a == $b ]
then
   echo "a 等于 b"
elif [ $a -gt $b ]
then
   echo "a 大于 b"
elif [ $a -lt $b ]
then
   echo "a 小于 b"
else
   echo "没有符合的条件"
fi

# for 循环
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done

# while
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done

# case... esac
echo -n "输入 1 到 5 之间的数字:"
read aNum
case $aNum in
    1|2|3|4|5) echo "你输入的数字为 $aNum!"
    ;;
    *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
        break
    ;;
esac
```

# shell function
```bash
funWithReturn(){
    echo "第0个参数为 $0 !"         # 当前的脚本 learn.sh
    echo "第一个参数为 $1 !"        # 1
    echo "第二个参数为 $2 !"        # 2
    echo "第三个参数为 $3 !"        # 3
    echo "所有参数 $* !"            # 1 2 3
    echo "参数个数 $# !"            # 3
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum ! $-"
    return $(($aNum+$anotherNum))
}
funWithReturn 1 2 3
echo "输入的两个数字之和为 $? !"
```
tips: $? 显示最后命令的退出状态或 函数的返回结果。命令状态0表示没有错误，其他任何值表明有错误。
tips: $(( )) 是用来作整数运算的。

# shell 文件引入
1. . filename   # 注意点号(.)和文件名中间有一空格
2. source filename

#! 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell

-----

# expect是一个免费的编程工具，用来实现自动的交互式任务，而无需人为干预。
```bash
#! /**/**/bin/expect
set timeout 30
set project [lindex $argv 0]
set passwd "123456"

spawn scp /**/**/${project}.zip name@ip:~/upload
expect {
        "密码："
        {
                send "$passwd\n"
        }
        "password"
        {
                send "$passwd\n"
        }
        eof
        {
                sleep 2
                        send_user "eof\n"
        }
}
send "exit\n"
expect eof

```