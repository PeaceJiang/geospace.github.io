---
title: SQL第一章：DDL数据定义语言
categories: 
  - 计算机
  - SQL
tags: [SQL笔记]
sidebar:
  - blogger
  - toc
copyright:
  type: type1
  author: null
  ref: null
  title: null
  url: null
date: 2023-08-08 23:33:54
description:
image:
---

数据定义语言（DDL）：Data Definition Language，用来定义数据库的对象，如数据表、视图、索引等。

<!-- more -->

### 数据库的增删改查、使用

```sql
# 创建数据库
CREATE DATABASE mydb1;
CREATE DATABASE IF NOT EXISTS mydb2;
# 创建指定字符集的数据库
CREATE DATABASE mydb3 CHARACTER SET UTF8;
CREATE DATABASE IF NOT EXISTS mydb2 SET UTF8;
/*针对不同字符集，MySQL指定了不同的排序规则（可以参考MySQL的帮助文档）。
例如：utf8字符集中指定的 utf8_general_ci 和 utf8_bin，对数据库中存储数据库的规则就有所不同。
      utf8_general_ci：ci是 case insensitive, 即 "大小写不敏感", a 和 A 会在字符判断中会被当做一样的。
      utf8_bin：将字符串每个字符串用二进制数据编译存储，区分大小写，而且可以存二进制的内容。*/

# 查询数据库
SHOW databases; # 查询所有数据库
SHOW CREATE DATABASE mydb3; # 查看指定数据库

# 修改数据库。只能修改数据库的字符集和排序规则，不能修改数据库名字
ALTER DATABASE mydb3 CHARACTER SET gbk COLLATE gbk_bin;

# 删除数据库
DROP DATABASE mydb3;

SELECT DATABASE(); # 查看正在使用的数据库
USE mydb1; # 使用规定的数据库
```

### 操作表的DDL

```sql
# 创建表
/*注意：在创建表之前，一定要先使用数据库（也就是说，表一定要创建在某个数据库中）*/
# CREATE TABLE 表名 (字段名1 数据类型,字段名2 数据类型,…,字段名n 数据类型)
CREATE TABLE student (
      id INT,
      name VARCHAR(20),
      birthday date
    ); # 创建student表包含id,name,age,sex字段

# 查看表
SHOW tables; # 查看所有表
DESC student; # 查看表结构
describe student; # 查看表结构
SHOW CREATE TABLE student; # 查看创建表的语句
CREATE TABLE s1 LIKE student; # 复制表结构，复制与student相同结构的s1表

# 修改表名
RENAME TABLE s1 TO st1; # RENAME TABLE 表名 TO 新表名

# 修改编码方式
	ALTER TABLE st1 CHARACTER SET gbk; # ALTER TABLE 表名 character set 字符集

# 删除表
DROP TABLE st1;
```

### 表单中的列操作

```sql
# 添加列
ALTER TABLE s1 ADD remark VARCHAR(20); # ALTER TABLE 表名 ADD 列名 类型

# 修改列类型
ALTER TABLE s1 MODIFY remark VARCHAR(100); # ALTER TABLE 表名 MODIFY 列名 新的类型

# 修改列名
ALTER TABLE s1 CHANGE remark intro varchar(30); # ALTER TABLE 表名 CHANGE 旧列名 新列名 类型

# 删除列
ALTER TABLE s1 DROP intro; # ALTER TABLE 表名 DROP 列名

```