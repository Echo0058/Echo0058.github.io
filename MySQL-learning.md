# MySQL
## Day 1 —— 环境搭建和初识数据库
> 参考教程链接：https://linklearner.com/learn/detail/70
> 环境搭建简易参考上述链接，针对windows，macOS和linux均有说明，且易上手

* 数据库 DataBase(DB)
* 数据库管理系统（Database Management System，DBMS）—— 管理数据库的计算机系统
<img width="604" alt="image" src="https://github.com/Echo0058/Echo0058.github.io/assets/105284489/e7fb4af9-7017-4cdd-949b-edc1c3ef2cc3">

1. Oracle Database：甲骨文公司的RDBMS
2. SQL Server：微软公司的RDBMS
3. DB2：IBM公司的RDBMS
4. PostgreSQL：开源的RDBMS
5. MySQL：开源的RDBMS
如上是5种具有代表性的RDBMS，其特点是由行和列组成的二维表来管理数据，这种类型的 DBMS 称为关系数据库管理系统（Relational Database Management System，RDBMS）。
 
* RDBMS的常见系统结构
![image](https://github.com/Echo0058/Echo0058.github.io/assets/105284489/95ada82e-bd21-412d-bb56-b7bb1d143370)
>ref：https://github.com/datawhalechina/wonderful-sql/blob/main/img/ch01/ch01.01%E7%B3%BB%E7%BB%9F%E7%BB%93%E6%9E%84.jpg

数据库存储的表结构类似于excel中的行与列
行：记录 
列：字段——代表表中存储的数据项目
单元格，一个单元格只能输入一条记录
SQL是为操作数据库而开发的语言

>“完全基于标准 SQL 的 RDBMS 很少，通常需要根据不同的 RDBMS 来编写特定的 SQL 语句，原则上，本课程介绍的是标准 SQL 的书写方式。”

SQL 语句
-------

SQL（Structured Query Language）是一种用于管理和操作关系型数据库的标准化查询语言。它允许用户通过简单的语句来执行各种操作，如插入、更新、删除和查询数据。

SQL 语句可以分为三类：
1. DDL ：DDL（Data Definition Language，数据定义语言） 用来创建或者删除存储数据用的数据库以及数据库中的表等对象。DDL 包含以下几种指令。

* CREATE ： 创建数据库和表等对象
* DROP ： 删除数据库和表等对象
* ALTER ： 修改数据库和表等对象的结构

2. DML :DML（Data Manipulation Language，数据操纵语言） 用来查询或者变更表中的记录。DML 包含以下几种指令。

* SELECT ：查询表中的数据
* INSERT ：向表中插入新数据
* UPDATE ：更新表中的数据
* DELETE ：删除表中的数据

3. DCL ：DCL（Data Control Language，数据控制语言） 用来确认或者取消对数据库中的数据进行的变更。除此之外，还可以对 RDBMS 的用户是否有权限操作数据库中的对象（数据库表等）进行设定。DCL 包含以下几种指令。

COMMIT ： 确认对数据库中的数据进行的变更
ROLLBACK ： 取消对数据库中的数据进行的变更
GRANT ： 赋予用户操作权限
REVOKE ： 取消用户的操作权限

-------
SQL书写规则：
* 分号结尾
* SOL不区分关键字大小写，但 **插入到表中的数据是区分大小写的** 
* win 系统默认不区分表名及字段名的大小写、
* linux / mac 默认严格区分表名及字段名的大小写
* 常数的书写方式是固定的 
    'abc', 1234, '26 Jan 2010', '10/01/26', '2010-01-26'......
* 单词需要用半角空格或者换行来分隔，**不能使用全角空格作为单词的分隔符**，否则会发生错误，出现无法预期的结果。


### 数据库的创建

```sql
# CREATE DATABASE < 数据库名称 > ;
CREATE DATABASE shop;
```

1. **创建表格**：
   用于创建数据库中的新表格。语法如下：
   ```sql
   CREATE TABLE table_name (
       column1 datatype1 constraint,
       column2 datatype2 constraint,
       ...
   );
   ```
```sql
CREATE TABLE product
(product_id CHAR(4) NOT NULL,
 product_name VARCHAR(100) NOT NULL,
 product_type VARCHAR(32) NOT NULL,
 sale_price INTEGER ,
 purchase_price INTEGER ,
 regist_date DATE ,
 PRIMARY KEY (product_id));
```
![image](https://github.com/Echo0058/Echo0058.github.io/assets/105284489/cc296e00-a31e-48e5-8728-cb31a90efe46)
>ref：https://github.com/datawhalechina/wonderful-sql/raw/main/img/ch01/ch01.03%E5%95%86%E5%93%81%E8%A1%A8%E5%92%8C%E5%88%97%E5%90%8D%E5%AF%B9%E5%BA%94%E5%85%B3%E7%B3%BB.png

**命名规则**
* 只能使用半角英文字母、数字、下划线（_）作为数据库、表和列的名称
* 名称必须以半角英文字母开头

### 数据类型的指定
数据库创建的表，所有的列都必须指定数据类型，每一列都不能存储与该列数据类型不符的数据。
* INTEGER 整数
* CHAR 长字符串（当列中存储的字符串长度达不到最大长度的时候，使用半角空格进行补足，由于会浪费存储空间，所以一般不使用）、
* VARCHAR 可变长度字符串 （定长字符串在字符数未达到最大长度时会用半角空格补足，但可变长字符串不同，即使字符数未达到最大长度，也不会用半角空格补足。）
* DATE 日期

### 约束
约束是除了数据类型之外，对列中存储的数据进行限制或者追加条件的功能。

* NOT NULL 是非空约束，即该列必须输入数据。
* PRIMARY KEY是主键约束，代表该列是唯一值，可以通过该列取出特定的行的数据。


### 表的删除和更新
* 删除：

删除的表是无法恢复的，只能重新插入，请执行删除操作时要特别谨慎。
```sql
DROP TABLE <表名> ;
DROP TABLE product;
```

* 添加列 

  ALTER TABLE < 表名 > ADD COLUMN < 列的定义 >;
  添加一列可以存储100位的可变长字符串的 product_name_pinyin 列
```sql
ALTER TABLE product ADD COLUMN product_name_pinyin VARCHAR(100);
```

* 删除列
  ALTER TABLE product DROP COLUMN product_name_pinyin;
```sql
ALTER TABLE product DROP COLUMN product_name_pinyin;
```

* 删除表中特定的行（语法）
```sql
-- 一定注意添加 WHERE 条件，否则将会删除所有的数据
DELETE FROM product WHERE COLUMN_NAME='XXX';
```

ALTER TABLE 语句和 DROP TABLE 语句一样，执行之后无法恢复。误添加的列可以通过 ALTER TABLE 语句删除，或者将表全部删除之后重新再创建。 【扩展内容】

* 清空表内容
  TRUNCATE TABLE TABLE_NAME
**优点：相比drop / delete，truncate用来清除数据时，速度最快。**

* 数据的更新
```
UPDATE <表名>
   SET <列名> = <表达式> [, <列名2>=<表达式2>...]  
 WHERE <条件>  -- 可选，非常重要
 ORDER BY 子句  --可选
 LIMIT 子句; --可选
```
**使用 update 时要注意添加 where 条件，否则将会将所有的行按照语句修改**
e.g.
```sql
-- 修改所有的注册时间
UPDATE product
   SET regist_date = '2009-10-10';  
-- 仅修改部分商品的单价
UPDATE product
   SET sale_price = sale_price * 10
 WHERE product_type = '厨房用具';  
```
**使用 UPDATE 也可以将列更新为 NULL（该更新俗称为NULL清空）。此时只需要将赋值表达式右边的值直接写为 NULL 即可。**
```sql
-- 将商品编号为0008的数据（圆珠笔）的登记日期更新为NULL  
UPDATE product
   SET regist_date = NULL
 WHERE product_id = '0008';  
```

>和 INSERT 语句一样， UPDATE 语句也可以将 NULL 作为一个值来使用。 **但是，只有未设置 NOT NULL 约束和主键约束的列才可以清空为NULL。**如果将设置了上述约束的列更新为 NULL，就会出错，这点与INSERT 语句相同。

**多列更新——UPDATE 语句的 SET 子句支持同时将多个列作为更新对象。**
```sql
-- 基础写法，一条UPDATE语句只更新一列
UPDATE product
   SET sale_price = sale_price * 10
 WHERE product_type = '厨房用具';
UPDATE product
   SET purchase_price = purchase_price / 2
 WHERE product_type = '厨房用具';

-- 上述代码可执行但较为繁琐，可通过合并简化，如下所示

-- 合并后的写法
UPDATE product
   SET sale_price = sale_price * 10,
       purchase_price = purchase_price / 2
 WHERE product_type = '厨房用具';  
```

>SET 子句中的列不仅可以是两列，还可以是三列或者更多。


 * 插入数据 —— INSERT

INSERT INTO <表名> (列1, 列2, 列3, ……) VALUES (值1, 值2, 值3, ……);  

对表进行全列 INSERT 时，可以省略表名后的列清单。这时 VALUES子句的值会默认按照从左到右的顺序赋给每一列。

```sql
-- 先创建一个名为 productins 的表
CREATE TABLE productins
(product_id    CHAR(4)      NOT NULL,
product_name   VARCHAR(100) NOT NULL,
product_type   VARCHAR(32)  NOT NULL,
sale_price     INTEGER      DEFAULT 0,
purchase_price INTEGER ,
regist_date    DATE ,
PRIMARY KEY (product_id)); 

-- 包含列清单
INSERT INTO productins (product_id, product_name, product_type, sale_price, purchase_price, regist_date) VALUES ('0005', '高压锅', '厨房用具', 6800, 5000, '2009-01-15');
-- 省略列清单
INSERT INTO productins VALUES ('0005', '高压锅', '厨房用具', 6800, 5000, '2009-01-15');  
```

原则上，执行一次 INSERT 语句会插入一行数据。插入多行时，通常需要循环执行相应次数的 INSERT 语句。其实很多 RDBMS 都支持一次插入多行数据

```sql
-- 通常的INSERT
INSERT INTO productins VALUES ('0002', '打孔器', '办公用品', 500, 320, '2009-09-11');
INSERT INTO productins VALUES ('0003', '运动T恤', '衣服', 4000, 2800, NULL);
INSERT INTO productins VALUES ('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20');
-- 多行INSERT （ DB2、SQL、SQL Server、 PostgreSQL 和 MySQL多行插入）
INSERT INTO productins VALUES ('0002', '打孔器', '办公用品', 500, 320, '2009-09-11'),
                              ('0003', '运动T恤', '衣服', 4000, 2800, NULL),
                              ('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20');  
-- Oracle中的多行INSERT
INSERT ALL INTO productins VALUES ('0002', '打孔器', '办公用品', 500, 320, '2009-09-11')
           INTO productins VALUES ('0003', '运动T恤', '衣服', 4000, 2800, NULL)
           INTO productins VALUES ('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20')
SELECT * FROM DUAL;  
-- DUAL是Oracle特有（安装时的必选项）的一种临时表A。因此“SELECT *FROM DUAL” 部分也只是临时性的，并没有实际意义。  
```
   
INSERT 语句中想给某一列赋予 NULL 值时，可以直接在 VALUES子句的值清单中写入 NULL。**想要插入 NULL 的列一定不能设置 NOT NULL 约束。**
```sql
INSERT INTO productins (product_id, product_name, product_type, sale_price, purchase_price, regist_date) VALUES ('0006', '叉子', '厨房用具', 500, NULL, '2009-09-20');
```

还可以向表中插入默认值（初始值）。可以通过在创建表的CREATE TABLE 语句中设置DEFAULT约束来设定默认值。
```sql
CREATE TABLE productins
(product_id CHAR(4) NOT NULL,
（略）
sale_price INTEGER
（略）	DEFAULT 0, -- 销售单价的默认值设定为0;
PRIMARY KEY (product_id));  
```

可以使用INSERT … SELECT 语句从其他表复制数据。
```sql
-- 将商品表中的数据复制到商品复制表中
INSERT INTO productcopy (product_id, product_name, product_type, sale_price, purchase_price, regist_date)
SELECT product_id, product_name, product_type, sale_price, purchase_price, regist_date
  FROM Product;
```
所参考教程用表插入数据sql如下：
```sql
- DML ：插入数据
STARTTRANSACTION;
INSERT INTO product VALUES('0001', 'T恤衫', '衣服', 1000, 500, '2009-09-20');
INSERT INTO product VALUES('0002', '打孔器', '办公用品', 500, 320, '2009-09-11');
INSERT INTO product VALUES('0003', '运动T恤', '衣服', 4000, 2800, NULL);
INSERT INTO product VALUES('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20');
INSERT INTO product VALUES('0005', '高压锅', '厨房用具', 6800, 5000, '2009-01-15');
INSERT INTO product VALUES('0006', '叉子', '厨房用具', 500, NULL, '2009-09-20');
INSERT INTO product VALUES('0007', '擦菜板', '厨房用具', 880, 790, '2008-04-28');
INSERT INTO product VALUES('0008', '圆珠笔', '办公用品', 100, NULL, '2009-11-11');
COMMIT;
```

* 索引
索引可以大大提高MySQL的检索速度。

索引创建了一种有序的数据结构，采用二分法搜索数据时，其复杂度为 1 ，1000多万的数据只要搜索23次，其效率是非常高效的。

创建索引：
```sql
CREATE TABLE mytable(  
 
ID INT NOT NULL,   
 
username VARCHAR(16) NOT NULL,  
 
INDEX [indexName] (username(length))  
 
);
-- or
-- 方法1
CREATE INDEX indexName ON table_name (column_name)

-- 方法2
ALTER table tableName ADD INDEX indexName(columnName)
```

索引分类：
1. 主键索引——建立在主键上的索引被称为主键索引，一张数据表只能有一个主键索引，索引列值不允许有空值，通常在创建表时一起创建。
2. 唯一索引——建立在UNIQUE字段上的索引被称为唯一索引，一张表可以有多个唯一索引，索引列值允许为空，列值中出现多个空值不会发生重复冲突。
3. 普通索引——建立在普通字段上的索引
4. 前缀索引——前缀索引是指对字符类型字段的前几个字符或对二进制类型字段的前几个bytes建立的索引，而不是在整个字段上建索引。前缀索引可以建立在类型为char、varchar、binary、varbinary的列上，可以大大减少索引占用的存储空间，也能提升索引的查询效率。
5. 全文索引——利用“分词技术”实现在长文本中搜索关键字的一种索引。
```sql
SELECT * FROM article WHERE MATCH (col1，col2，...) AGAINST (expr [ search _ modifier ])
```
**如果可能，请尽量先创建表并插入所有数据后再创建全文索引，而不要在创建表时就直接创建全文索引，因为前者比后者的全文索引效率要高。**
6. 单列索引
7. 联合索引（复合索引，多列索引）


## 练习题
1. 编写一条 CREATE TABLE 语句，用来创建一个包含表 1-A 中所列各项的表 Addressbook （地址簿），并为 regist_no （注册编号）列设置主键约束
   
2. 假设在创建练习1.1中的 Addressbook 表时忘记添加如下一列 postal_code （邮政编码）了，请编写 SQL 把此列添加到 Addressbook 表中。
```sql
CREATE TABLE Addressbook
(regist_no INTEGER NOT NULL, 
 name VARCHAR(128) NOT NULL,
 address VARCHAR(256) NOT NULL,
 tel_no CHAR(10) ,
 mail_address CHAR(20) ,
 PRIMARY KEY (regist_no));
 
-- 忘记添加如下一列 postal_code （邮政编码）了，
-- 请编写 SQL 把此列添加到 Addressbook 表中
ALTER TABLE Addressbook ADD COLUMN postal_code VARCHAR(8) NOT NULL
```

3. 填空题
 请补充如下 SQL 语句来删除 Addressbook 表。

 (DROP) table Addressbook;

 或者 TRUNCATE TABLE TABLE_NAME;

4. 判断题

 是否可以编写 SQL 语句来恢复删除掉的 Addressbook 表？

 否，删除操作不能恢复   
