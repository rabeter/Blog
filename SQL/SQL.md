
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
2. INSERT
3. delect
4. distinct(过滤)




### 检索数据(SELECT)

select prod_name from Products;
从Products表中检索prod_name的列
select prod_id, prod_name,prod_price from prosucts;
检索多列
select * from products；
检索所有的列(性能问题)，在列名位置情况下可使用查看所有表名。

#### 过滤相同值(distinct)



select distinct prod_id from Products;
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


### 字段(field)
计算字段在表中不是真是存在的，经过其他字段统计得来的

1. 拼接(+或||)
 SQL Server 使用+   Oracle、PostgreSQL、SQLite使用||
select name + country from table order by name;
