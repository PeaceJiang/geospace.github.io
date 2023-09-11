---
title: SQL第三章：DQL数据查询语言
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
date: 2023-09-11 23:15:47
description:
image:
---

DQL：Data Query Language，用来查询数据库中的数据。

<!-- more -->

### 单表查询

**简单查询**

```sql
# 查询表中的所有数据
SELECT * FROM student;
Select id,name,age,sex,address from student; # 列出所有字段

# 指定列查询
Select id,name from student; # 列出需要查询的字段

# 别名查询（在查询时，给查询的列或表起一个其他的（一般是稍短的名字，或为了防止重复）名字就叫做别名。使用别名的好处是方便查看和处理查询到的数据。）
SELECT 字段名1 AS 别名, 字段名2 AS 别名... FROM 表名;
SELECT NAME AS '姓名', age AS '年龄' FROM student; # 设定别名并查询
```

<aside>
💡 别名查询注意事项

- 查询时给表取别名目前还看不到效果，需要到多表查询的时候才能体现出其好处。
- AS关键字可以省略。
</aside>

```sql
# 查询并去除重复记录
SELECT DISTINCT 字段名 FROM 表名
SELECT DISTINCT name,age,address FROM student # 去除选择字段均相同的重复记录
```

<aside>
💡 查询去重：
查询去重并不会改变原表的数据，仅仅会提取原表中选择字段的非重复数据

</aside>

```sql
# 查询结果参与运算（+ - * /）
# 在查询语句中，查询的列的可以和其他值做数学运算(加、减、乘、除等)。运算结果只会影响展示，不会影响表中的数据。
SELECT 列名1 + 固定值 FROM 表名
SELECT 列名1 + 列名2 FROM 表名
```

### 条件查询

**运算符**

在查询条件中，可以使用多种比较运算符来表示查询条件。
= 等于，> 大于，<小于，<=小于等于，>=大于等于， <>或!=不等于

**逻辑运算符**

and(&&) 多个条件同时满足
or(||) 多个条件其中一个满足
not(!) 不满足

```sql
# 查询age大于35或性别为男的学生(两个条件其中一个满足)
SELECT * FROM student WHERE age>35 OR sex='男';
```

**指定范围内查询 in**

```sql
SELECT 字段名 FROM 表名 WHERE 字段 in (数据1, 数据2...); # in里面的每个数据都会作为一次条件，只要满足条件的就会显示。
SELECT * FROM student WHERE id IN (1,3,5); # 这里的IN 相当于将OR条件的连接 SELECT * FROM student WHERE id=1 OR id=3 OR id=5; 

```

**模糊查询**

MySQL通配符有两个：

- %: 表示0个或多个字符(任意个字符)
- _: 表示一个字符

```sql
# 模糊查询姓马的学生
SELECT * FROM student WHERE NAME LIKE '马%';
# 查询姓马，且姓名有三个字的学生
SELECT * FROM student3 WHERE NAME LIKE '马__';

# 查询姓名中包含'德'字的学生
SELECT * FROM student3 WHERE NAME LIKE '%德%';
```

**空值查询**

查询某个字段为空（null）的数据，不是使用=null（null和任何值都不相等），而是使用is null来进行判断。

```sql
# 查询english成绩为null的学生信息
SELECT * FROM student WHERE english IS NULL
```

### 排序

通过ORDER BY子句，可以将查询出的结果进行排序，排序只影响显示结果，不会影响数据库中数据的顺序。

**单列排序**

```sql
/*
SELECT 字段名 FROM 表名 [WHERE 条件] ORDER BY 字段名 [ASC|DESC]; 
ASC: 升序，默认是升序 
DESC: 降序
*/

# 查询所有数据，使用年龄降序排序：
SELECT * FROM student3 ORDER BY age DESC;
```

**组合排序**

组合排序就是先按第一个字段进行排序，如果第一个字段相同，才按第二个字段进行排序，依次类推。

```sql
SELECT 字段名 FROM 表名 [WHERE 条件] ORDER BY 字段名1 [ASC|DESC],字段名2 [ASC|DESC];

# 查询所有数据，在年龄降序排序的基础上，如果年龄相同再以数学成绩降序排序：
SELECT * FROM student3 ORDER BY age DESC, math DESC;
```

### 函数

**单行函数**：是指对于每一行数据进行计算后得到一行输出结果。SQL单行函数根据数据类型分为字符函数、数字函数、日期函数、转换函数等。

```sql
SELECT ABS(-1) -- 返回 x 的绝对值,返回1
SELECT CEIL(1.5) -- 返回大于或等于 x 的最小整数（向上取整）返回2
SELECT FLOOR(1.5) -- 返回小于或等于 x 的最大整数（向下取整）返回1
SELECT RAND() --返回 0 到 1 的随机数0.93099315644334
SELECT ROUND(1.23456) --四舍五入取整，返回1
SELECT CONCAT("SQL ", "Runoob ", "Google ", "Facebook") AS ConcatenatedString; --合并字符串
SELECT LOCATE('st','myteststring'); -- 返回字符串a在字符串b中的位置，5
SELECT LOWER('RUNOOB') -- 所有字母变小写 runoob
SELECT UPPER("runoob"); -- 所有字母变大写 RUNOOB
SELECT REPLACE('abc','a','x') --字符串替换 xbc
SELECT SUBSTRING("RUNOOB", 2, 3) AS ExtractString; -- 字符串切片 UNO
SELECT TRIM(' RUNOOB ') AS TrimmedString; -- 去除字符串前后多余的空格'RUNOOB'
SELECT reverse('dog'); -- 反转字符串，返回god
SELECT now(); -- 返回当前系统时间
SELECT sysdate(); -- 返回当前系统时间,(包括年月日时分秒)
SELECT curdate(); -- 返回当前日期(年月日)
SELECT curtime(); -- 返回当前时间(时分秒)
SELECT MONTH('2020-11-12'); -- 返回参数中的月份
SELECT WEEK('2020-11-12'); -- 返回参数日期是一年中的第几个星期
SELECT DAY('2020-11-12'); -- 返回参数中的日值
SELECT DATE_ADD('2020-11-12 12:11:22',interval 3 MONTH) # date_add(date,INTERVAL expr type)date 参数是合法的日期表达式。expr 参数是您希望添加的时间间隔。
/*type 参数可以是下列值：MICROSECOND
SECOND
MINUTE
HOUR
DAY
WEEK
MONTH
QUARTER
YEAR
SECOND_MICROSECOND
MINUTE_MICROSECOND
MINUTE_SECOND
HOUR_MICROSECOND
HOUR_SECOND
HOUR_MINUTE
DAY_MICROSECOND
DAY_SECOND
DAY_MINUTE
DAY_HOUR
YEAR_MONTH*/
```

**流程控制函数**