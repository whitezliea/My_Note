# MySQL基础

## 1 开题篇

数据库的好处：

1. 持久化数据到本地
2. 可以实现结构化存储，方便管理



## 2 数据库的相关概念

DBMS、DB、SQL

- DB：数据库（database），存储数据的“仓库”。它保存了一系列有组织的数据。
- DBMS：数据库管理系统（Database Management System）。数据库是通过DBMS创建和操作的容器
- SQL：结构化查询语言（Structure Query Language）：专门用来与数据库通信的语言。

SQL的优点：

1. 不是某个特定数据库供应商专有的用语言，几乎所有的DBMS都支持SQL
2. 简单易学
3. 虽然简单，但实际上是一种强有力的语言，灵活使用其语言元素，可以进行非常复杂和高级的数据库操作



## 3 数据库存储数据的特点

特点：

1. 数据放到表中，表再放到库中。  数据------->表-------->数据库
2. 一个数据中可以有多个表，每个表都有一个的名字，用来标识自己。**表名具有唯一性。**
3. 表具有一些特性，这些特性定义了数据在表中如何存储，类似Java中“类”的设计。
4. 表由列组成，我们也称之为**字段**。所有表都是由一个或者多个列组成的，每一列类似Java中的“属性”。
5. 表中的数据是按行存储，每一行类似于Java中的“对象”。



## 4 初始化MySQL

### 4.1 MySQL简介

MySQL的优点：

- 成本低：开放源代码，一般可以免费试用
- 性能高：执行很快
- 简单：很容易安装和使用

DBMS分为两类：

- 基于共享文件系统的DBMS（微软的Access）

- 基于客户机 - 服务器的DBMS（MySQL、Oracle、SqlServer）

  

### 4.2 MySQL服务的启动和停止

Linux下:

启动：sudo /etc/init.d/mysql start

停止：sudo /etc/init.d/mysql stop



### 4.3 MySQL服务的登录和退出

Linux下的：

登录：sudo mysql -u `用户名` -p -h `主机名` -P `端口`

Enter Password：`密码`

退出：exit; 或者  quit;

### 4.4 MySQL的常见命令和语法规范

常见命令：

1. 查看当前所有的数据库 

   

   ```sql
   SHOW DATABASES;
   ```

2. 打开指定的库

   ```sql
   USE 表名;
   ```

3. 查看当前库的所有表

   ```sql
   SHOW TABLES;
   ```

4. 查看其他库的所有表

   ```sql
   SHOW TABLES FROM 库名;
   ```

5. 创建表

   ```sql
   CREATE TABLE 表名(
   列名 列类型,
   列名 列类型,
   ......
   )
   ```

6. 查看表结构

```sql
DESC 表名;
```

7. 查看MySQL服务器版本

```sql
SELECT version();
```



语法规范：

1. 命令不区分大小写；表名，库名等参数区别大小写；建议命令关键字大写，表名，列名小写
2. 每条命令最好用分号结尾
3. 每条命令根据需要，可以进行缩进或者换行
4. 注释

```sql
# 单行注释
-- 单行注释
/*多行
注释
*/
```



## 5 DQL语言的学习

### 5.1基础查询

```SQL
#选择数据库
USE myemployees;
#显示表结构
DESC departments;
#进阶1：基础查询
/*
语法：
 SELECT 查询列表 FROM 表名;

特点：
查询列表是：表中的字段、常量值、表达式、函数
查询的结果是一个虚拟的表格。
*/

#1.查询表中的单个字段
SELECT last_name FROM employees;

#2.查询表中多个字段
SELECT last_name,salary,email FROM employees;

#3.查询表中的所有字段
SELECT * FROM employees;

#4.查询常量值
SELECT 100;
SELECT 'abc';

#5.查询表达式
SELECT 100*90;

#6.查询函数
SELECT VERSION();

#7.起别名
/*优点：
(1)便于理解
(2)如果查询的字段由重名的情况，使用别名可以区分开来
*/
SELECT 100%98 AS 结果;
#方式一：
SELECT last_name AS 姓,first_name AS 名 FROM employees;
#方式二：
SELECT last_name  姓,first_name 名 FROM employees;
#别名可以用引号括起来，不建议带空格
SELECT salary AS "out_put" FROM  employees;

#8.去重
#案例：查询员工表中涉及到的所有的部门编号
SELECT DISTINCT department_id FROM employees;

#9.+号的作用
/*
java中的+号：
(1)运算符，两个操作数都为数值型
(2)连接符，只要有一个操作数为字符串

mysql中的+号：
仅仅只有一个作用：运算符
SELECT 100+90;   两个操作数都为数值型，则做加法运算
SELECT '123'+90; 其中一方为字符型，试图将字符型数值转换成数值型
                      如果转换成功，则继续做加法运算
SELECT 'john'+90;     如果转换失败，则将字符型数值转换成0
SELECT NULL+90;    只要其中一方为null，则结果肯定为null
*/
#案例：查询员工名和姓连接成一个字段，并显示为 姓名
#拼接函数 SELECT CONCAT('a','b','c');
SELECT
       CONCAT(last_name,' ',first_name) AS 姓名
FROM employees;

#案例显示表employees的全部列，各个列之间用逗号连接，列头显示成OUU_PUT
#注意：NULL与其他字段拼接，结果为NULL
SELECT 
        IFNULL(commission_pct,0)AS 奖金率
FROM
        employees;
#---------------------------------------------------------
SELECT 
        CONCAT('first_name',',','last_name',',','job_id',',',IFNULL(commission_pct,0)) AS OUT_PUT
FROM
        employees;

```

条件查询

排序查询

常见函数

分组函数

分组查询

连接查询

子查询

分页查询

union联合产线

## 6 DML语言的学习

插入语句

修改语句

修改语句

删除语句

## 7 DOL语言的学习

库和表的管理

常见数据类型介绍

常见约束

## 8 TCL语言的学习

事务和事务处理

## 9 视图的讲解

## 10 存储过程和函数

## 11 流程控制函数

