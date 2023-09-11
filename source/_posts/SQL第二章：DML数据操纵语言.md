---
title: SQL第二章：DML数据操纵语言
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
date: 2023-09-11 23:13:50
description:
image:
---



DML: Data Manipulation Language，用来在数据库表中更新，增加和删除记录。

<!-- more -->

### 插入数据表中的记录

```sql
# 插入记录
INSERT INTO student (id, name, age, sex) VALUES (1, '张三', 20, '男'); # 向学生表中添加 id, name, age, sex数据
```

![Untitled](https://pic.imgdb.cn/item/64ff2c8e661c6c8e5492cf24.png)

<aside>
💡 **插入记录注意事项**
值与字段必须对应，个数相同，类型相同
值的数据大小必须在字段的长度范围内 varchar()
除了数值类型外，其它的字段类型的值必须使用引号引起（建议单引号）
如果要插入空值，可以不写字段，或者插入null

</aside>

```sql
# 不指定字段插入记录
INSERT INTO student VALUES (3, '王五', 18, '男', '北京'); # 此时按表的顺序自动插入
```

![Untitled](https://pic.imgdb.cn/item/64ff2c60661c6c8e5492c91f.png)

蠕虫复制（在已有的数据基础之上，将原来的数据进行复制，插入到对应的表中。）

```sql
# 创建student2表，student2结构和student表结构一样
CREATE TABLE student2 LIKE student;

# 将student表中的数据添加到student2表中
INSERT INTO student2 SELECT * FROM student
```

### 删除表记录

不带条件删除

```sql
# DELETE FROM 表名
DELETE FROM student; # 删除student表中的所有数据
```

带条件删除

```sql
# DELETE FROM 表名 WHERE 条件
DELETE FROM student WHERE id=3 # 带条件删除数据，删除id为3的记录
```

### 更新表记录

不带条件更新

```sql
# UPDATE 表名 SET 字段1=值1[,字段2=值2,,...,字段n=值n]
UPDATE student SET sex='女'; # 记录中所有性别字段都变成女
```

带条件更新（使用where语句）

```sql
# UPDATE 表名 SET 字段1=值1[,字段2=值2,,...,字段n=值n][where 条件]
UPDATE student SET sex='男' WHERE id=2; # 将id号为2的学生性别改成男
```