<!--
 * @Author: 二刚 wb-yangergang@cai-inc.com
 * @Date: 2022-11-27 21:52:49
 * @LastEditors: wb-yangergang
 * @LastEditTime: 2023-01-03 20:04:20
 * @FilePath: /doc/blog/source/_posts/OS/linux.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
---
title: linux
date: 2018/5/4
categories:
- OS
---
> 在Linux系统中，一切都是文件.

### 系统目录结构图
![file](https://www.runoob.com/wp-content/uploads/2014/06/d0c50-linux2bfile2bsystem2bhierarchy.jpg)


### 系统启动过程
1. 内核的引导。
  1.1 当计算机打开电源后，首先是BIOS开机自检，按照BIOS中设置的启动设备（通常是硬盘）来启动。
  1.2 操作系统接管硬件以后，首先读入 /boot 目录下的内核文件。
2. 运行 init。
  2.1 运行第一个进程 /sbin/init
  2.2 init 进程是系统所有进程的起点，你可以把它比拟成系统所有进程的老祖宗，没有这个进程，系统中任何进程都不会启动。
3. 确定运行级别
  3.1 init 程序首先是需要读取配置文件 /etc/inittab。里面配置了开机启动程序的运行级别，如 id:2:initdefault: 开机运行级别为2
4. 运行开机启动程序
  4.1 根据运行级别启动对应级别的程序
  4.2 每一级别对应的程序定义在 /etc/rc2.d 里，这里rc2 的 2 表示运行级别为 2 程序目录
  4.3 运行级别目录里的并不是真正的程序文件，而是链接文件，真正的程序放在 /etc/init.d 里
5. 用户登陆


### 计算机开机过程
1. BIOS 硬件自检
2. BIOS按照"启动顺序"，把控制权转交给排在第一位的储存设备
3. 读取该设备的第一个扇区（主引导记录）获取操作系统的位置（在那个主分区）
4. 读取该主分区的第一个扇区（卷引导记录）获得操作系统在分区中的哪个位置
5. 计算机加载操作系统

