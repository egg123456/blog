---
title: windows-command-line
date: 2018/5/14
categories:
- OS
---

### base
command|description
----|----
$ set path|查看path的环境变量值（准确的说是查看以path开头的环境变量）
$ set p=a12|设置变量p并赋值
$ echo %p%|显示变量p代表的字符串
$ cls|清除屏幕
$ ver|显示当前windows系统的版本号
$ winver|弹框显示当前windows系统信息
$ vol|显示当前分区的卷标
$ label|显示当前分区的卷标，同时提示输入新卷标
$ label c:system|设置c盘的卷标为system
$ time|显示或设置当前时间
$ date|显示或设置当前日期
$ title 正在做命令行测试|修改当前cmd窗口的标题栏文字为正在做命令行测试
$ prompt orz:|将命令提示符修改为orz:
$ print 1.txt|使用设置好的打印机来打印1.txt文本文件
$ call ff.bat|调用执行ff.bat脚本（ff.bat脚本执行完原脚本才会往下执行）
$ start|运行某程序或命令
$ pause|暂停批处理程序，并显示出：请按任意键继续....
$ color 02|设置当前cmd窗口背景色和前景色（前景色即为字体的颜色）无参回复默认

### 文件类
command|description
----|----
$ d:|跳转到d盘
$ cd folderPath|调到指定目录下
$ cd..|返回上一层目录
$ md/mkdir folderName|在当前目录下新建目录
$ rd/rmdir /s /q folderName|删除目录(/s参数表示不管有没内容都删除但会出现提示，再加上/q就不会提示)
$ type nul>filename.type|在当前目录下新建空文件
$ echo content>filename.type|在当前目录下新建有内容的文件
$ del filename.type|删除文件
$ del. /q|删除当前目录下的所有文件(/q参数表示不提示删除)
$ dir|显示当前目录下的子目录及文件信息
$ dir /b|只显示当前目录下的子目录及文件名
$ dir /ad|显示当前目录中的子文件夹
$ dir /a-d|显示当前目录中的文件
$ dir key*|显示当前目录下以key开头的文件和文件夹的信息
$ tree|显示当前目录之下的所有目录结构
$ ren oldname newname|将当前目录下的文件或文件夹重命名
$ copy key.txt c:\doc\key_bak.txt|将当前目录下的key.txt拷贝到c:\doc下，并重命名为key_bak.txt也可不重命名（若doc中也存在一个key_bak.txt文件，会询问是否覆盖）
$ type filename.type|显示文件内容
$ more filename.type|逐屏的显示当前目录下conf.ini的文本内容【空格：下一屏 q：退出 】
$ move sourcePath targetPath | 将文件或文件夹移动到目标文件夹下

# 高级
command|function
-------|--------
services.msc | 打开服务器面板
explorer.exe | 运行资源管理器--桌面？
shutdown.exe | 关机程序
mstsc.exe | 远程桌面连接

# 本机
command|function
-------|--------
winver | 系统版本
slmgr.vbs -xpr | 查看系统是否激活
regedit | 打开注册表
tasklist | 任务列表
netstat -ano | 进程占用端口列表
taskkill /pid 编号 /f | 杀掉进程
dxdiag | 获取系统cup 内存 显卡信息
Get-PhysicalDisk | powersell命令-获取磁盘信息（是否事ssd等）