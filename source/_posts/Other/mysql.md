---
title: mysql
date: 2018/5/13
categories:
- Other
---
> mysql 数据库中不仅有你创建的 database，还有其他保存整个数据库信息的相关 database。

# information_schema 存储整个数据库相关信息，如你创建的 database 的表名、表类型
tables 表 - 保存所有表的表名、类型。。。
columns 表 - 保存所有表的列名、数据类型。。。

### login
mysql -h localhost -u root －p
quit / exit

### databases
show databases

create database <databaseName>

drop database <databaseName>

use <databaseName>

select database()   // 其他语言的 print 功能 - 当前选择的数据库
select version()  // 其他语言的 print 功能 - 数据库版本
select now()    // 其他语言的 print 功能 - 当前时间
select ((4 * 4) / 10 ) + 25     // 计算器

----
### table

show tables // 显示当前使用的数据库中的所有表
select table_name from information_schema.tables where table_schema='database_name' and table_type='base table';

CREATE TABLE <tableName>(
    > id int(10) not null AUTO_INCREMENT,
    > name char(20) not null,
    > sex int(4) not null default '0',
    > PRIMARY KEY (id)
);
create table algorithm (id int(10) not null auto_increment, titleDesc TEXT not null, inputDesc TEXT not null, outputDesc TEXT not null, useCase TEXT not null, titleAnalysis TEXT not null, code TEXT not null, PRIMARY KEY (id));

select table_name from information_schema.tables where table_schema='csdb' and table_type='base table';

desc <tableName> / show columns from <tableName> // 表中的列信息
select column_name,data_type from information_schema.columns where table_schema='database_name' and table_name='table_name';

drop table <tableName>

insert into MyClass(id,name,score) values (1,'Tom',96.45),(2,'Joan',82.99), (2,'Wang', 96.59);

select * from <tableName> where id > 1 && sex = 1
SELECT * FROM students ORDER BY score DESC LIMIT 3 OFFSET 9; // paged query
SELECT * FROM students ORDER BY score DESC LIMIT 9,3; // paged query

delete from <tableName> where name = 'egg'

update <tableName> set name = 'yeg'
update <tableName> set name = 'liuZhi' where id=1;

alter table <tableName> add age int(1) not null default 18
alter table <tableName> modify password char(20);
alter table <tableName> drop age

rename table <oldTableName> to <newTableName>

-----
### use and grant

CREATE USER 'egg'@'localhost' IDENTIFIED BY 'password';
GRANT SELECT ON test.* TO 'egg'@'localhost';
<!-- modify password -->
ALTER USER root@localhost IDENTIFIED BY 'new_password';
<!-- modify password IDENTIFIED-->
ALTER USER root@localhost IDENTIFIED WITH mysql_native_password BY 'qwer1234';
<!-- refresh PRIVILEGES -->
FLUSH PRIVILEGES;


### plugin
INSTALL PLUGIN pluginName SONAME pluginName.os;


### timezone
SELECT TIMEDIFF(NOW(), UTC_TIMESTAMP); // look timeDiff(chian standard timeDiff is +8)

show variables like "%time_zone"; // look timezone variable value

set global time_zone="+8:00"; // 设置全局时区为北京时区，即东8区
set time_zone="+8:00"; // 修改当前会话时区
flush privileges; // 立即生效


### configure env variable for mac
<!-- configure env variable -->
sudo vim .bash_profile
export PATH=${PATH}:/usr/local/mysql/bin
<!-- run env variable -->
source .base_profile
<!-- zsh: command not found: mysql -->
sudo ln -fs /usr/local/mysql/bin/mysql mysql


### dataType
> MySQL 支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型。
1. 数值类型

类型 | 大小 |	范围（有符号）|	范围（无符号）|	用途
----|-----|-------------|-------------|-----
TINYINT	| 1 Bytes |	(-128，127) |	(0，255) | 小整数值
SMALLINT | 2 Bytes | (-32 768，32 767) | (0，65 535) | 大整数值
MEDIUMINT | 3 Bytes | (-8 388 608，8 388 607) | (0，16 777 215) | 大整数值
INT或INTEGER | 4 Bytes | (-2 147 483 648，2 147 483 647) | (0，4 294 967 295) | 大整数值
BIGINT | 8 Bytes | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807) | (0，18 446 744 073 709 551 615) | 极大整数值
FLOAT | 4 Bytes | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) |	0，(1.175 494 351 E-38，3.402 823 466 E+38) | 单精度 浮点数值
DOUBLE | 8 Bytes | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308)	| 双精度 浮点数值
DECIMAL | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值 | 依赖于M和D的值 | 小数值

2. 日期和时间类型

类型 | 大小( bytes) | 范围 | 格式 | 用途
-----|--------------|------|------|-----
DATE | 3 | 1000-01-01/9999-12-31 | YYYY-MM-DD | 日期值
TIME | 3 | '-838:59:59'/'838:59:59' | HH:MM:SS | 时间值或持续时间
YEAR | 1 | 1901/2155 | YYYY | 年份值
DATETIME | 8 | '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59' | YYYY-MM-DD hh:mm:ss | 混合日期和时间值
TIMESTAMP | 4	| '1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07' UTC 结束时间是第 2147483647 秒，北京时间 2038-1-19 11:14:07，格林尼治时间 2038年1月19日 凌晨 03:14:07 | YYYY-MM-DD hh:mm:ss	 | 混合日期和时间值时间戳

3. 字符串

类型 | 大小 | 用途
-----|------|----
CHAR | 0-255 bytes | 定长字符串
VARCHAR | 0-65535 bytes | 变长字符串
TINYBLOB | 0-255 bytes | 不超过 255 个字符的二进制字符串
TINYTEXT | 0-255 bytes | 短文本字符串
BLOB | 0-65 535 bytes | 二进制形式的长文本数据
TEXT | 0-65 535 bytes | 长文本数据
MEDIUMBLOB | 0-16 777 215 bytes | 二进制形式的中等长度文本数据
MEDIUMTEXT | 0-16 777 215 bytes | 中等长度文本数据
LONGBLOB | 0-4 294 967 295 bytes	| 二进制形式的极大文本数据
LONGTEXT | 0-4 294 967 295 bytes | 极大文本数据


# export data 
1. export table data
  SELECT * FROM runoob_tbl INTO OUTFILE '/tmp/runoob.txt'
2. export database data
  + 导出整个数据库结构和数据
    mysqldump -h localhost -P 3306 -uroot -p123456 database > test.sql
  + 导出单个数据表结构和数据
    mysqldump -h localhost -P 3306 -uroot -p123456 database table > test.sql
  + 导出整个数据库结构（不包含数据）
    mysqldump -h localhost -P 3306 -uroot -p123456 -d database > test.sql
  + 导出单个数据表结构（不包含数据）
    mysqldump -h localhost -P 3306 -uroot -p123456 -d database table > test.sql
  + 说明：
    + 如果是本机操作，其中 -h localhost -P 3306 可以不需要
    + -P 参数，是大P，且有空格；不同于后面密码的小p，没有空格

# import data
source test.sql

# 事务
### 事务的ACID原则
A/Atomicity：原子性
C/Consistency：一致性
I/Isolation：独立性/隔离性
D/Durability：持久性

### 事务隔离机制分为了四个级别
①Read uncommitted/RU：读未提交
②Read committed/RC：读已提交
③Repeatable read/RR：可重复读
④Serializable：序列化/串行化


## tool all-mysql-client 


# my.ini database config file
```txt
[mysqld]
; 设置3306端口
port=3306
; 设置mysql的安装目录
basedir=D:\programFile\mysql-9.0.1-winx64
; 设置mysql数据库的数据的存放目录
datadir=D:\programFile\mysql-data
; 允许最大连接数
max_connections=200
; 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
; 服务端使用的字符集默认为UTF8
character-set-server=utf8
; 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
; 默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password
[mysql]
; 设置mysql客户端默认字符集
default-character-set=utf8
[client]
; 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```

 root@localhost: tLibUX(sT1BB

 D:\doc\myApp\text.sql


 INSTALL PLUGIN mysql_native_password SONAME 'mysql_native_password.so';

D:\doc\myApp\text.sql