---
title: Timestamp与Datatime区别
date: 2018-12-16 14:50:40
tags: SQL
header-img: "/img/if/DSC01830.jpg"
subtitle: "最近遇到了写时间的bug"
---

总结来说就是
1. 时间戳（Timestamp）不管哪种表示指向的都是同一个时间点。DATETIME 类型的值在不同的时区下显示相同
    ```
    mysql> show variables like 'time_zone';
    +---------------+--------+
    | Variable_name | Value  |
    +---------------+--------+
    | time_zone     | +08:00 |
    +---------------+--------+
    1 row in set (0.001 sec)

    mysql> CREATE TABLE `test` (
        ->       `id` int(11) NOT NULL AUTO_INCREMENT,
        ->       `timestamp` timestamp NULL DEFAULT NULL,
        ->       `datetime` datetime DEFAULT NULL,
        ->      PRIMARY KEY (`id`)
        ->     ) ENGINE=InnoDB;
    Query OK, 0 rows affected (1.17 sec)

    mysql> insert into `test` (`id`,`timestamp`, `datetime`) values (1,now(), now());
    Query OK, 1 row affected (0.35 sec)

    mysql> select * from test_table
        -> ;
    +----+---------------------+---------------------+
    | id | timestamp           | datetime            |
    +----+---------------------+---------------------+
    |  1 | 2018-12-06 10:49:37 | 2018-12-06 10:49:37 |
    +----+---------------------+---------------------+
    1 row in set (0.00 sec)

    mysql> set time_zone = 'UTC';
    Query OK, 0 row affected (0.00 sec)

    mysql> select * from test_table
        -> ;
    +----+---------------------+---------------------+
    | id | timestamp           | datetime            |
    +----+---------------------+---------------------+
    |  1 | 2018-12-06 02:49:37 | 2018-12-06 10:49:37 |
    +----+---------------------+---------------------+
    1 row in set (0.00 sec)

    mysql> 
    ```
2. 写代码上的区别
    - DataTime

    显示格式	YYYY-MM-DD HH:mm:ss

    显示范围	1601-01-01 00:00:00 到 9999-12-31 23:59:59

    应用场景	当业务需求中需要精确到秒时，可以用这个时间格式

    fastjson注解	@JSONField(format=”yyyy-MM-dd HH:mm:ss”)
    - DataTime

    显示格式	YYYY-MM-DD HH:mm:ss

    显示范围	1601-01-01 00:00:00 到 9999-12-31 23:59:59

    应用场景	当业务需求中需要精确到秒或者毫秒时，或者该系统用于不同时区，可以用这个时间格式

    fastjson注解	@JSONField(format=”yyyy-MM-dd HH:mm:ss:SSS”)
