#  TIMESTAMP 和 DATETIME些许不同

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
|  1 | 2018-12-06 10:49:37 | 2018-12-06 10:49:37 |
+----+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> 
```

