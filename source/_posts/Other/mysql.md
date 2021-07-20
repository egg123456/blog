<!--
 * @Author: wb-yangergang
 * @Date: 2021-05-23 12:04:46
 * @LastEditors: wb-yangergang
 * @LastEditTime: 2021-07-20 16:40:21
 * @Description: file content
-->
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
    > id int(10) not null,
    > name char(20) not null,
    > sex int(4) not null default '0',
);

select table_name from information_schema.tables where table_schema='csdb' and table_type='base table';

desc <tableName> / show columns from <tableName> // 表中的列信息
select column_name,data_type from information_schema.columns where table_schema='database_name' and table_name='table_name';

drop table <tableName>

insert into MyClass values (1,'Tom',96.45),(2,'Joan',82.99), (2,'Wang', 96.59);

select * from <tableName> where id > 1 && sex = 1

delete from <tableName> where name = 'egg'

update <tableName> set name = 'yeg'

alter table <tableName> add age int(1) not null default 18
alter table <tableName> drop age

rename table <oldTableName> to <newTableName>

-----
### use and grant

CREATE USER 'egg'@'localhost' IDENTIFIED BY 'password';
GRANT SELECT ON test.* TO 'egg'@'localhost';
