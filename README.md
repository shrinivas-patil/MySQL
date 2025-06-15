# MySQL

mysql> CREATE TABLE customer1
    -> (
    -> acc_no INT PRIMARY KEY,
    -> name VARCHAR(50) NOT NULL,
    -> acc_type VARCHAR(50) NOT NULL DEFAULT 'Saving'
    -> );
Query OK, 0 rows affected (0.02 sec)

mysql> desc customer1;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| acc_no   | int         | NO   | PRI | NULL    |       |
| name     | varchar(50) | NO   |     | NULL    |       |
| acc_type | varchar(50) | NO   |     | Saving  |       |
+----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> insert into customer1(acc_no, name)
    -> values (1001,'Raju'),(1002,'Sham');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from customer1;
+--------+------+----------+
| acc_no | name | acc_type |
+--------+------+----------+
|   1001 | Raju | Saving   |
|   1002 | Sham | Saving   |
+--------+------+----------+
2 rows in set (0.00 sec)

mysql> insert into customer1(acc_no, name)
    -> values (1001,'baburoa');
ERROR 1062 (23000): Duplicate entry '1001' for key 'customer1.PRIMARY'
mysql>
mysql>
mysql>
mysql>  insert into customer1(name)
    -> values('Paul');
ERROR 1364 (HY000): Field 'acc_no' doesn't have a default value
mysql>
mysql>
mysql>
mysql> insert INTO customer1(acc_no, name)
    -> values(null,'paul');
ERROR 1048 (23000): Column 'acc_no' cannot be null
mysql>
