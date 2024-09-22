---
title: linux-command-line
date: 2018/5/14
categories:
- shortcut
---

### base
command|description
-------|-----------
du | 列举目录大小信息
du -h | 适合人类阅读的
du -s | 只显示总计大小，不显示具体信息
du -sh | 适合人类阅读的方式显示总计大小
cat -n filePath | 带行号显示文件
less filePath | 分页显示文件
head -n 5 filepath | 只显示文件前5行
tail -n 5 filepath | 只显示文件最后5行
touch filename | 创建文件
mkdir foldername | 创建目录
mkdir -p one/two/three | 递归创建目录
mv *.txt folder | 文件或目录移动
cp -r folderone foldertwo | 复制整个目录
rm -r folder | 递归删除整个目录

### user
command|description
-------|-----------
useradd useName | 添加新用户
passwd useName | 修改用户密码
userdel lion | 只会删除用户名，不会从/home中删除对应文件夹
userdel lion -r	| 会同时删除/home下的对应文件夹

### other
command|description
-------|-----------
find . -name "syslog"	| 当前目录以及子目录下通过名称查找文件
find /var -size 10M | /var 目录下查找文件等于 10M 的文件
find /var -size +10M | /var 目录下查找文件大小超过 10M 的文件
find /var -size -10M | /var 目录下查找文件大小不超过 10M 的文件
find . -name "file" -type f | 只查找当前目录下的file文件
find . -name "file" -type d | 只查找当前目录下的file目录
find -name "*.jpg" -delete | 删除当前目录以及子目录下所有.jpg为后缀的文件，不会有删除提示，因此要慎用
find . -type f | 列出当前目录及子目录下的所有文件
find . -type f -atime +365 | 查找最后访问时间草果 365 天的文件
find . -type f -mtime -7 | 找出7天内修改过的文件
find . -type f -perm 777 | 按权限找文件
find -type f -user yang | 按文件所属的用户搜索
find . -type f -atime +365 -exec rm -rf {} \; | 删除最后访问时间超过 365 天的文件，{}是查找结果的占位符


### origin manage
```sh
# 备份系统自带 yum 源配置文件 
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
# 下载阿里云的 yum 源配置文件到 /etc/yum.repos.d/CentOS7
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
# 生成缓存
yum makecache
```

### operation
输入本机密码后，打开hosts文件，键盘输入 i （插入），修改hosts文件后，按 esc 键退出,再按shift+：键，再输入w和q，保存退出