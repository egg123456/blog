---
title: fileTransform
date: 2018/5/5
categories:
- protocol
---

# scp
从本地 下载远程文件 或者目录 到 本地
scp user@host:/path/file /localpath
scp -r user@host:/dirpath /localpath

从本地 上传文件 或目录 到 远程主机
scp localfile user@host:/dirpath 
scp -r localdir user@host:/dirpath 


# sftp
是一个交互式文件传输程式。它类似于 ftp, 但它进行加密传输，比FTP有更高的安全性。

sftp fyt@202.206.64.33 或者 fyt@www.hebust.edu.cn 回车提示输入密码。进入提示符
sftp>

如果登陆远程机器不是为了上传下载文件，而是要修改远程主机上的某些文件。可以
ssh fyt@202.206.64.33 （其实sftp就是ssh 的一个程式。）

在sftp中get表示下载即得到； put表示上传即放置
sftp> get filepath localfilepath
sftp> put localfilepath filepath

在sftp 命令提示符中 cd pwd ls rm rmdir mkdir 这些命令都可以使用。如果要操作本机则在命令前加 l , 即 lls lrm.
要离开sftp，用exit 或quit、 bye 均可。详细情况可以查阅 man sftp.

如果觉得在命令行模式下不太方便，可以 sudo apt-get install gftp。
在图形界面下操作就简便多了

tips: windows 用户需确认是否安装ssh服务，当然如果你安装git，可直接打开git bash 使用以上命令

