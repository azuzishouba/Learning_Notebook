# MySql笔记
## CREATE DATABASE
* create database  (databasename) 创建数据库
* -- 代表MySQL注释
## USE关键字
* use (database_name) 使用哪一个数据库
## SELECT关键字
* select (cloumn_name) 选择表中需要的列，通常要和from搭配使用
    >seletct (cloumn_name)

    >from (table_name)
### AS关键字
* AS (cloumn_name)给指定列一个别名
### DISTINCT关键字
* DISTINCT (column_name)用于查询中去除重复结果，返回唯一值
### UNIQUE关键字
* UNIQUE 用于表的定义当中,确保值唯一
## WHERE关键字
*  WHERE用于过滤搜索的结果
    >seletct (cloumn_name)

    >from (table_name)

    >where (constraint_condition)
## 逻辑运算符
* AND,OR,NOT 表示与或非
## 关系运算符
* BETWEEN...AND,IN,表示在两者值之间，是否在对象里
## LIKE 关键字
* LIKE '查询内容'
    * LIKE '%field' 表示以查询内容开头
    * LIKE 'field%' 表示以查询内容结尾
    * LIKE '%field%' 表示查询内容在中间
## REGEXP正则表达式
* REGEXP 等同于LIKE,但是比LIKE功能更强
* REGEXP 'field' = LIKE 'field'
* REGEXP '^field' = LIKE '%field' 
* REGEXP 'field$' = LIKE 'field%' 
* REGEXP 'field|mac|rose'  | 可以表示或,查询只要符合三者中任意一个即可
* REGEXP '[gim]e' 表示只要符合方括号中的一个即可,ge,ie,me都可。REGEXP 'e[fmq]' 同理表示ef，em，eq都可
* REGEXP '[a-h]e' 符合a到h中的一个就可以
## NULL关键字
* IS NULL 查询列名中为空的值
## ORDER BY关键字
* ORDER BY (column_name) 给指定列排序，默认升序
    * DESC 将升序变为降序
## LIMIT关键字
* LIMIT (number) 表示限制取多少条数据
* LIMIT (pass_number,number) 表示跳过多少条数据，再取多少条数据
## INNER JOIN内连接
>select * 

>from orders o 可以简写为o

>join customers c 要连接的表

>>on o.customer_id=c.customer_id  两表中共有的列，这样才可以拼接
## SELF JOIN自连接
>select e.employee_id,e.first_name,m.first_name AS manager 自连接同列名需要指定表名

>from employee e 可以简写为e

>join employee m 可以简写为m,连接自己本身

>>on  e.reports_to=m.employee_id
## 多表连接
>select o.order_id,o.order_date,c.first_name,c.last_name,os.name AS status

>from orders o 简写为o

>join customers c 简写为c

>>on  o.customer_id=c.customer_id 寻求两张表共同列

>join order_status os 简写为os 

>>on  o.status=os.order_status_id 

需求拼接后的表共同列
## 复合连接情况
* 在某些情况下，一张表有两个主键，这类似于二维数组，两个数字才能代表唯一性
> select *  

>from order_items oi

>join order_item_notes oin

>>on oi.order_id=oin.order_id

>>and oi.product.id=oin.product_id 

当表中有两个主键时，都需要进行连接，使用and来指定两个连接条件
## 隐式连接
> select *  

>from order o，customers c

>where o.customer_id=c.customer_id

尽量不使用隐式连接，忘记where条件后，就进行交叉连接，最好使用显示连接，join...on指定连接条件
## 外连接
OUTER JOIN 外连接分为左连接和右连接
### 左连接
LEFT JOIN 左连接:无论连接条件是否为真,无条件保留左表所有的数据再进行连接
>select c.customer_id,c.first_name,o.order_id

>from customers c 左连接保留左表所有记录，左表为customers

>left join orders o 右表为orders

>>on c.customer_id=o.customer_id
order by c.customer_id
### 右连接
RIGHT JOIN 右连接:无论连接条件是否为真,无条件保留右表所有的数据再进行连接
>select c.customer_id,c.first_name,o.order_id

>from orders o 

>left join customers c 右连接保留右表所有记录,右表为c

>>on c.customer_id=o.customer_id
order by c.customer_id
## 多表进行外连接
尽量都是用左连接,代码可读性更强
## 自身外连接
>select e.employee_id,e.first_name,m.first_name AS manager 自连接同列名需要指定表名

>from employee e 可以简写为e

>left join employee m 这种情况下员工都有经理,但是没有经理的信息,所以进行左表外连接也就是左连接，来显示经理信息

>>on  e.reports_to=m.employee_id
## USING关键字
如果两张表有相同的列名,可以用using来代替on
>select o.order_id,c.first_name

>from orders o 

>join customers c

>>using (customer_id)

等同于on c.customer_id=o.customer_id
>order by c.customer_id


在需要多重连接的情况下同样可以使用using,using (column_name1,column_name2)
> select *  

>from order_items oi

>join order_item_notes oin

>>using (order_id,product_id)
## 交叉连接
进行交叉连接就是把两张表所有记录进行笛卡尔积,可以视作叉乘
> select c.first_name as customer,p.name as product 

>from customers c

>cross join products p

>order by c.first_name
## UNION联合
合并两个或多个查询的结果,默认去除重复行,想包含重复行可以UNION ALL,查询时须保持列数,列数据类型一致,第一个选择的列名会代表联合后的列名
> select order_id,order_date,'Active' AS status

>from orders

>where order_date>='2019-01-01'

>UNION 表示两者查询的合并

> select order_id,order_date,'Archived' AS status

>from orders

>where order_date<'2019-01-01'
## 列的属性
* int 类型,表示数据是整形,不含小数点
* varchar 类型,字符型,varchar(50),var代表variable,表示可变,最多可以有50个字节,当数据只有5个字节时,不会用空格填充,节省了空间
* char 类型,字符型,和varchar不同的是分配好空间后,不足的会用空格填充
* primary key 主键,代表数据的唯一标识
* not null,表示不能为空
* auto increment,表示自增
* default,表示分配的默认值
## 插入数据
### 插入单行数据
>insert into customers (first_name,last_name,birth_date,address,city,state) 可不指定列名,就需要给所有列数据

>values('john','smith','1990-01-01','address','city','CA')

### 插入多条数据
>insert into shippers (name)

>values('shippers1'),('shippers2'),('shippers3')

插入多条数据时,用逗号分隔开
### 插入层次行
>insert into orders (customer_id,order_date,status)

>values(1,'2019-01-02',1);

>insert into order_items

>values(LAST_INSERT_ID(),1,1,2.95),(LAST_INSERT_ID(),1,1,2.95)

LAST_INSRET_ID()用来获取刚刚插入数据的id
## 表格的浅复制
浅复制只复制数据，表的结构不复制
>create table orders_archived AS

>select *

>from orders

## 子查询
>insert into orders_archived

>select *

>from orders

>where order_date < '2019-01-01'

* exercies:
    >create table invoices_archived AS  
 
    >select *

    >from invoices i

    >join clients c

    >>USING (client_id)

    >where payment_date is not null
## 更新数据
### 更新单行数据
>update invoices

>set payment_total=70,payment_date=null

>where invoice_id=1
### 更新多行数据
在mysql workbench中，不允许一下子更改多条数据，需要在preference,sql editor，取消safe mode,重新开启workbench就能更改多条数据
### 利用子查询更新数据
>update invoices

>set payment_total=invoice_total*0.5,payment_date=due_date

>where client_id=

>>(select client_id

>>from clients

>>where name='myworks')

>update invoices

>set payment_total=invoice_total*0.5,payment_date=due_date

>where client_id IN

>>(select client_id

>>from clients

>>where status IN ('CA','NY')) 多条语句下用IN


子查询的语句需要带括号,mysql会优先执行括号内语句
## 删除数据
>delete from 

>where client_id=

>>(select *

>>from clients

>>where name='myworks')

## MYSQL中的事务
* 事务的四个特性:
  * 原子性：一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。
  * 一致性：在事务开始之前和事务结束以后，数据库的完整性没有被破坏。
  * 隔离性：数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。
  * 持久性：事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

*在 MySQL 命令行的默认设置下，事务都是自动提交的，即执行 SQL 语句后就会马上执行 COMMIT 操作。因此要显式地开启一个事务务须使用命令 BEGIN 或 START TRANSACTION，或者执行命令 SET AUTOCOMMIT=0，用来禁止使用当前会话的自动提交。*

MYSQL 事务处理主要有两种方法：

1. 用 BEGIN, ROLLBACK, COMMIT 来实现

    BEGIN 或 START TRANSACTION：开用于开始一个事务。
    ROLLBACK 事务回滚，取消之前的更改。
    COMMIT：事务确认，提交事务，使更改永久生效。

2. 直接用 SET 来改变 MySQL 的自动提交模式:

    SET AUTOCOMMIT=0 禁止自动提交
    SET AUTOCOMMIT=1 开启自动提交

BEGIN 或 START TRANSACTION -- 用于开始一个事务：
>BEGIN; -- 或者使用 START TRANSACTION;

COMMIT -- 用于提交事务，将数据的更改永久提交：
>COMMIT;

ROLLBACK -- 用于回滚事务，撤销到未进行任何操作之前或者savepoint：
>ROLLBACK;

SAVEPOINT -- 用于在事务中设置保存点，以便稍后能够回滚到该点：
>SAVEPOINT savepoint_name;

ROLLBACK TO SAVEPOINT -- 用于回滚到之前设置的保存点：
>ROLLBACK TO SAVEPOINT savepoint_name;

