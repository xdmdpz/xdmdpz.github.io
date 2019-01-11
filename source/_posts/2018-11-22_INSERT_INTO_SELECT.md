---
title: INSERT INTO SELECT
date: 2018-11-22 13:40:40
tags: SQL
header-img: "img/header_img/archive-bg.png"
subtitle: "按照最近项目的开发习惯"
---


我们经常会遇到需要表复制的情况，如将一个table1的数据的部分字段复制到table2中，或者将整个table1复制到table2中，这时候我们就要使用SELECT INTO 和 INSERT INTO SELECT 表复制语句了。

语句形式为：

`Insert into Table2(field1,field2,...) select value1,value2,... from Table1`

或者：

`Insert into Table2 select  *  from Table1`

注意：
1. 要求目标表Table2必须存在，并且字段field,field2...也必须存在

2. 注意Table2的主键约束，如果Table2有主键而且不为空，则 field1， field2...中必须包括主键

3. 注意语法，不要加values，和插入一条数据的sql混了，不要写成:

	`Insert into Table2(field1,field2,...) values (select value1,value2,... from Table1)`
4. 由于目标表Table2已经存在，所以我们除了插入源表Table1的字段外，还可以插入常量。


