# MySql笔记
## CREATE DATABASE
* create database  (databasename) 创建数据库
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

