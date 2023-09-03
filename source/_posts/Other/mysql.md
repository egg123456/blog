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

creat table <tableName>(
    > id int(10) not null AUTO_INCREMENT,
    > name char(20) not null,
    > sex int(4) not null default '0',
    > PRIMARY KEY (id)
);

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
