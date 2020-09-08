# SQL基础

## 概要

结构化查询语言(Structured Query Language)简称SQL,sql是用来操作关系型数据库的语言,ISO作为互联网的老大哥,同样也为sql定制了标准,但是并不是所有组织都会完全遵守老大哥的标准.MySQl数据库的语句照搬到SQL Server就可能出现错误,因此考虑代码移植和兼容真的是DBA(Database Administrator)们头疼的事情.

不过我们不用管那么多,**本文是基于MySql的标准sql.**

sql分为很多种语言,包括DDL,DML,DCL等等,我们会依次介绍.

## 语法

1. sql语句必须以分号结尾

2. sql不区分关键字大小写(建议大写)

3. 注释有两种

   ```mysql
   #单行注释
   /*
     多
     行
     注
     释
   */
   ```
## 前提准备

为了更好演示sql语法,请粘贴以下代码到SQLyog,F9执行,到时候做演示使用.

```mysql
CREATE DATABASE  IF NOT EXISTS Girls;
CREATE TABLE Lolis(
	loli_name VARCHAR(20),
	age INT,
	nature ENUM('傲娇','天然呆','病娇')
);
```



# 基本语句

## 使用数据库

```mysql
USE <数据库名字>;
```

## 查看当前用的哪个数据库

```sql
select database();
```



# DDL (数据定义语言)

数据库模式定义语言(Data Definition Language),简称DDL,是用来定义创建数据库和表的语言

## 数据库的创建

```sql
CREATE DATABASE IF NOT EXISTS <数据库名称> ;
```

## 数据库字符集的修改

```sql
ALTER DATABASE <数据库名称> CHARACTER SET gbk; 
```

## 删库(跑路)

```sql
DROP DATABASE IF EXISTS <数据库名称>;
```

## 表的创建

下面是一个最简单的表,其中前面是变量名,后面是类型,刚好和其他语言相反.

```sql
CREATE TABLE book(
	id INT,
	book_name VARCHAR(20),
	price DOUBLE,
	author_id INT,
	publishData DATETIME
);
```

### 数据类型的指定

就像上面那张表,sql的数据类型有很多种,

#### 整数

```mysql
TINYINT  		#(1BYTE)
SMALLINT    #(2BYTE)
MEDIUMINT   #(3BYTE)
INT         #(4BYTE)
BIGINT      #(8BYTE) 
```

也可以在整数后面指定无符号型

```mysql
INT UNSIGNED
```

#### 浮点数

```mysql
FLOAT    #(4BYTE)

```



#### 字符

```mysql
CHAR(最大长度)
VARCHAR(最大长度)
```

这两种字符类型在使用前都必须指定最大长度,但是CHAR类型在数据没有填满的时候自动补充半角空格,而VARCHAR是可变长字符串,如果没有到达最大长度,那么它会自动缩小占用空间,但是也不能超过最大长度.

#### 枚举

用ENUM声明

```mysql
CREATE TABLE table_enum
(
	e1 ENUM('a','b','c')
);
```



### 添加表的约束

#### 主键约束



#### 非空约束

#### 默认约束

## 表的修改

```sql
ALTER TABLE 表名 <具体操作> <操作的对象>;
```

可以看到,ALTER有着很多种操作,接下来详细介绍一下.

### 修改表的类名和数据类型

```sql
ALTER TABLE book CHANGE COLUMN price book_price (DOUBLE);
```

### 修改表的数据类型和约束

```sql
ALTER TABLE book MODIFY COLUMN publishData TIMESTAMP;
ALTER TABLE book MODIFY COLLATE id INT PRIMARY KEY;
```

### 增加新的列

```sql
ALTER TABLE book ADD COLUMN number INT;
```

### 删除列

```sql
ALTER TABLE book DROP COLUMN number;
```

### 删除主键

```sql
ALTER TABLE book DROP PRIMARY KEY;
```

#新增表级约束的主键
ALTER TABLE book ADD CONSTRAINT pk PRIMARY KEY (id);





#表的重命名
ALTER TABLE book RENAME TO books;

#表的删除
DROP TABLE book;

#description 的缩写，和那个descending不一样
DESC book;


SHOW TABLES;

#复制表的结构，但是不会复制数据
CREATE TABLE copy_table LIKE book;

#复制结构+全部元素
CREATE TABLE copy_table2 
SELECT * FROM book;

#也可以复制一部分
CREATE  TABLE copy_table3
SELECT id,price
FROM book;

#也可以设一个恒假的值，从而不会复制到值，只是复制部分结构,
CREATE TABLE copy_table4
SELECT id,price
FROM book
WHERE 0;

# DML (数据操作语言)



```sql



DESC employees;


SELECT first_name,first_name FROM employees;


SELECT IFNULL(commission_pct,0) AS 奖金率 FROM employees;
#IFNULL 用于判断NULL值，第一个为判断的对象第二个为用于替换的值

SELECT 
	*
FROM   
	employees	
WHERE
	NOT(`department_id`>=90 AND`department_id`<=110) OR salary>15000;


#like is fuzzy search
/*
	like通常与通配符搭配使用 
	last_name LIKE 'a%';表示前面a开头，后面可以有若干字符
	last_name LIKE 'a_s%';表示a开头，第三个字母为s，之后可以有若干字符

*/

SELECT 
	*
FROM   
	employees	
WHERE
	last_name LIKE 'a_s%';
```



```sql
#谁的工资比Abel高
#首先要查Abel的工资，之后再查谁的比他高
SELECT *
FROM employees
WHERE salary>(
	SELECT salary
	FROM employees
	WHERE	last_name='Abel');
	
#查询最低工资大于 50号部门最低工资的 部门id和最低工资
#1,先查50号部门的最低工资
SELECT	MIN(salary)
FROM  employees
WHERE employees.`department_id`=50
#2,再查询每个部门的最低工资
SELECT MIN(salary)
FROM employees
GROUP BY `department_id`
#3,最后再筛选
SELECT MIN(salary)
FROM employees
GROUP BY `department_id`
HAVING MIN(salary)>(#注意这种>符号，后面只能跟标量子查询
	SELECT	MIN(salary)
	FROM  employees
	WHERE employees.`department_id`=50
);


#查询location_id=1400或1700的部门的所有员工姓名
#我现在有点明白了，子查询就是差=查定语，先查部门，再查部门的员工姓名
#1
select	departments.`department_id`
from departments
where location_id in (1400,1700);
#2
select last_name
from employees
where department_id=(
	SELECT	departments.`department_id`
	FROM departments
	WHERE location_id IN (1400,1700)
);

#查询 其他部门中 比job_id为IT_PROG部门任意工资低的员工 的员工号 姓名 job_ID和salary
#1,找到job_id为IT_PROG部门的员工
select employee_id
from employees
where job_id='IT_PROG'

#2,找到该部门员工的最小工资
select	min(salary)
from employees
where employee_id in (
	SELECT employee_id
	FROM employees
	WHERE job_id='IT_PROG'
);


#3，找到其他部门中比最小工资还小的员工
select employee_id,last_name,job_id,salary
from employees
where salary<(
	select	min(salary)
	from employees
	where employee_id = any(
		SELECT employee_id
		FROM employees
		WHERE job_id='IT_PROG'
		)

);

#查询员工编号最小，而且工资最高的员工
select *
from employees
where employee_id=(
	select min(employee_id)
	from employees)
and salary=(
	select max(salary)
	from employees)	;
#可以简写为
select *
from employees
where (employee_id,salary)=(
	select min(employee_id),max(salary)
	from employees)	;

select count(*)
from employees;
```



# DQL (数据查询语言)

## 普通查询

### 单/多列查询

```mysql
SELECT 
  <列名1>,
  <列名2>
FROM
  <表名>;
```

### 查询所有列

```mysql
SELECT * FROM <表名>;
```

### 为查询取别名

```mysql
SELECT 
  <列名1>  AS <别名1>,
  <列名2>  AS <别名2>
FROM
  <表名>;
```

### 删除重复元素

```mysql
SELECT DISTINCT <列名> FROM <表名>;
```

### 常数查询

```mysql
SELECT "Hello World";
SELECT 0721;
```



## 条件查询

SELECT语句可以加上WHERE子句来指定查询的条件.

```mysql
SELECT 
  <列名1>,
  <列名2>
FROM
  <表名>
WHERE 
	<条件表达式>;
```



# TCL  (事务控制语言)