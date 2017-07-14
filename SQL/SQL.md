
## SQL

数据库(database)：保存有组织的的数据容器。

表(table):某种特定类型数据的结构化清单。

列(column):表中的一个字段。存储特定相同的信息。

行(row):记录一组完整的信息。也成为记录。

### 主键
唯一标识每一行，通常只能是一列。
 满足条件：
 1. 任意两行都不具有相同的主键值
 2. 每一行必须有主键值(不允许为NULL)
 3. 主键列中的值不允许修改和更新
 4. 主键值不能够重用(木行从表中删除，它的主键不能够赋值到新行)

### 注释
-- 行内注释
 /*  块注释*/
 
### 关键字
1. SELECT
2. INSERT INTO
3. delete
4. update
5. create database
6. create table
7. alter database(修改数据库)
8. alter table(修改表)
9. create index(创建索引)
10. drop index(删除索引)
4. distinct(过滤)




### 检索数据(SELECT)

select prod_name from Products;
从Products表中检索prod_name的列
select prod_id, prod_name,prod_price from prosucts;
检索多列
select * from products；
检索所有的列(性能问题)，在列名位置情况下可使用查看所有表名。

#### 检索不同数据(delect distinct)

**select distinct** prod_id from Products;
distinct 作用于所有的列

#### 限制结果
TOP限制返回行数量
select TOP 5 prod_name from products;

Oracle
SELECT prod_name FROM Products WHERE ROWNUM <=5;
MySQL、PostgreSQL、SQLLite
select prod_name from products limit 5;

#### 排序(order by)
select prod_name from Produtcs order by prod_name;
保证order by为最后一条语句

select prod_id,prod_price,prod_name from products order by prod_price,prod_name;
= select prod_id,prod_price,prod_name from products order by 2,3;
多列排序(按照先后顺序)(相对位置)

select prod_id from products order by prod_price DESC
降序排序(DESC)

### 过滤数据(where)
select prod_name from products where prod_price <=10;
过滤出price<=10的数据

> 优化数据库后可以更快速有效地对数据进行过滤。而让客户端应用（或开发语言）处理数据库的工作将会极大地影响应用的性能，并且使所创建的应用完全不具备可伸缩性。此外，如果在客户端过滤数据，服务器不得不通过网络发送多余的数据，这将导致网络带宽的浪费。

select rpod_name,prod_price from products where **prod_price between 5 and 10;**
过滤price在5与10之间的数据
select prod_name from products prod_name **is NULL;**
过滤非空数据

### 组合
and or
select prod_name, prod_price from products 
where (id = "dell" or id ="hp") and prod_price >=10;
and 优先级比or高

select prod_name, prod_price from products 
where (id = "dell" or id ="hp") and prod_price >=10;
= select prod_name, prod_price from products 
where **id in ("dell" ,"hp")** and prod_price >=10;
in 操作指定范围，功能与or相同

not
select prod_name from products 
where not id = ‘dell’ order by prod_name;
= select prod_name from products 
where id != ‘dell’ order by prod_name;

### 通配符(like)
用来匹配值的一部分特殊字符，一般只能应用于文本字符串。
>SQL的通配符很有用。但这种功能是有代价的，即通配符搜索一般比前面讨论的其他搜索要耗费更长的处理时间。

> 通配符不会匹配NULL

1. %: 表示字符出现任意次数
select prod_name from products where **prod_name like ‘fish%’;**
匹配以fish开头的字符串
select prod_name from products where ** prod_name like ‘% bean bag%’；**
匹配任何位置有**bean bag**的字符串
2. _ :只匹配单个字符
select prod_name from products where **prod_name like ’_inch‘;**
匹配首个任意的inch字符
3. [] : 指定字符集(SQL Server支持)
select prod_name from products where id ** like '[ABC]';**
匹配ABC其中之一的字符
4. [^]:指定非字符集
select prod_name from products where id ** like '[^ABC]';**
不匹配ABC字符

### 别名
表别名
列别名

### 字段(field)
计算字段在表中不是真是存在的，经过其他字段统计得来的

1. 拼接(+或||)
 SQL Server 使用+   Oracle、PostgreSQL、SQLite使用||
select name + country from table order by name;
将原来的列组合起来形成新的字段
2. 使用别名
 select name + country ** as title** from table order by name;
将新的字段命名以便以后使用
 
### 函数
1. trim/rtrim/ltrim去空格
2. upper 转化大写
3. len返回长度
4. lower转化小写
5. left 返回字符左边字符串
6. right返回字符串右边字符串
7. substr(Oracle、PostgreSQL、SQLite) / substring(MySQL、SQLServer)提取字符串
8. convert 数据类型转换
9. abs 绝对值
10. cos/sin/tan
11. exp 指数
12. pi 返回PI
13. sqrt 平方根
14. 聚集函数
15. avg 平均
16. count统计行数
17. max/min/sum

### 分组
1. group by
select id, count(*) as num_prods from products group by id;

id | num_prod
---|---
 1 | 5
 2 | 3
 4 | 6
 
2. having
select id, count(*) as order from oders group by id having count(*) >=5;
id | num_prod
---|---
 1 | 5
 4 | 6
 
####  select 子句顺序
 select  from  where （group by） having （order by）

### 	联结表(join)
用一条select 语句检索出关联的多表成为联结
1. INNER JOIN：如果表中有至少一个匹配，则返回行
2. LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行
3. RIGHT JOIN：即使左表中没有匹配，也从右表返回所有的行
4. FULL JOIN：只要其中一个表中存在匹配，则返回行

select ven_name, prod_name,prod_price from Vendors, products 
**where Vendors.vend_id = products.vend_id;**

#### 内联结
内联结也称为等值联结，基于两个表之间的相等测试。
select vend_name , prod_name,prod_price
from **vendors inner join products on Vendors.vend_id=products.vend_id;**
与前一条结果相同

### 表别名
1. 缩短SQL语句
2. 允许在一条语句中多次使用相同的表
SELECT cust_name, cust_contact
FROM Customers AS C, Orders AS O, OrderItems AS OI
WHERE C.cust_id = O.cust_id AND OI.order_num = O.order_num AND prod_id = 'RGAN01';

#### 自联结
引用的同一个表
SELECT c1.cust_id, c1.cust_name, c1.cust_contact
FROM Customers AS c1, Customers AS c2
WHERE c1.cust_name = c2.cust_name
 AND c2.cust_contact = 'Jim Jones'; 
#### 自然联结
检索第一个表中的所有字段
SELECT C.*, O.order_num, O.order_date,
 OI.prod_id, OI.quantity, OI.item_price
FROM Customers AS C, Orders AS O, OrderItems AS OI
WHERE C.cust_id = O.cust_id
 AND OI.order_num = O.order_num
 AND prod_id = 'RGAN01';
#### 外联结
将没有关联行的表联结在一起
SELECT Customers.cust_id, Orders.order_num
FROM Customers** left outer join** Orders
 ON Customers.cust_id = Orders.cust_id; 
 Customers 与Orders没有关联行
 =SELECT Customers.cust_id, Orders.order_num
FROM Customers **right outer join** Orders
 ON **Orders.cust_id = Customers.cust_id;**

###  union

### select into(复制)

select * into newTable
from oldTable
复制表中内容到新表中

### 插入(insert into)
insert into table_name (column1,column2) values (val1,val2);
向table_name中插入数据


### 更新(update)

update table_name set col1=val1,col2=val2
**where col=val;**
一定包含where子句，防止作用于全局更新


### 删除(delete)

delete from table_name
**where col = val;**


### create database(创建数据库)
create database my_db;

### create table(创建表)



 
 