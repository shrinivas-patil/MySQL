----------------------------------------------
EXERCISEE 1
-----------------------------------------------
*    Create a database - bank_db
*    Create a table - employees
            emp_id
            name
            desig
            dept
*    emp_id column should not allow duplicate and null values, Value of emp_id column should auto increment
*    name column should not contain null value
*    desig column should have default value as 'Probation'

--------------------------------------------------
SOLUTION
--------------------------------------------------
mysql> create database bank_db;
Query OK, 1 row affected (0.02 sec)

mysql> use bank_db;
Database changed
mysql> CREATE TABLE Emplyees(
    -> emp_id INT PRIMARY KEY AUTO_INCREMENT,
    -> name VARCHAR(50) NOT NULL,
    -> desig VARCHAR(50) NOT NULL DEFAULT 'Probation',
    -> dept VARCHAR(50) NOT NULL
    -> );
Query OK, 0 rows affected (0.09 sec)

mysql> desc Employees;
ERROR 1146 (42S02): Table 'bank_db.employees' doesn't exist
mysql> desc Emplyees;
+--------+-------------+------+-----+-----------+----------------+
| Field  | Type        | Null | Key | Default   | Extra          |
+--------+-------------+------+-----+-----------+----------------+
| emp_id | int         | NO   | PRI | NULL      | auto_increment |
| name   | varchar(50) | NO   |     | NULL      |                |
| desig  | varchar(50) | NO   |     | Probation |                |
| dept   | varchar(50) | NO   |     | NULL      |                |
+--------+-------------+------+-----+-----------+----------------+
4 rows in set (0.01 sec)

mysql> INSERT INTO Emplyees(emp_id,name,desig,dept)
    -> values(101,'Raju','Manager','Loan');
Query OK, 1 row affected (0.02 sec)

mysql> select * from Emplyees;
+--------+------+---------+------+
| emp_id | name | desig   | dept |
+--------+------+---------+------+
|    101 | Raju | Manager | Loan |
+--------+------+---------+------+
1 row in set (0.00 sec)

mysql> INSERT INTO Emplyees(name,desig,dept)
    -> VALUES
    -> ('Sham','Cashier','Cash'),
    -> ('Paul','Associate','Lone'),
    -> ('Alex','Accountant','Account'),
    -> ('Victor','Associate','Deposite');
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> select * from Emplyees;
+--------+--------+------------+----------+
| emp_id | name   | desig      | dept     |
+--------+--------+------------+----------+
|    101 | Raju   | Manager    | Loan     |
|    102 | Sham   | Cashier    | Cash     |
|    103 | Paul   | Associate  | Lone     |
|    104 | Alex   | Accountant | Account  |
|    105 | Victor | Associate  | Deposite |
+--------+--------+------------+----------+
5 rows in set (0.00 sec)

mysql> select emp_id,name from Emplyees;
+--------+--------+
| emp_id | name   |
+--------+--------+
|    101 | Raju   |
|    102 | Sham   |
|    103 | Paul   |
|    104 | Alex   |
|    105 | Victor |
+--------+--------+
5 rows in set (0.00 sec)

mysql>mysql> select desig AS 'Design' from Emplyees;
+------------+
| Design     |
+------------+
| Manager    |
| Cashier    |
| Associate  |
| Accountant |
| Associate  |
+------------+

----------------------------------------------------------------------------------------------------------------------
ADDING EXTRA COLUMN AS A LASTNAME 
-------------------------------------------------------------------------------------------------------------------

Enter password: **********
mysql> use bank_db;
Database changed
mysql> select * from emplyees;
+--------+--------+------------+----------+
| emp_id | name   | desig      | dept     |
+--------+--------+------------+----------+
|    101 | Raju   | Manager    | Loan     |
|    103 | Paul   | Associate  | Loan     |
|    104 | Alex   | Accountant | IT       |
|    105 | Victor | Associate  | Deposite |
+--------+--------+------------+----------+
4 rows in set (0.02 sec)

mysql> ALTER TABLE Emplyees
    -> ADD COLUMN last_name VARCHAR(50)
    -> After name;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | NULL      | Manager    | Loan     |
|    103 | Paul   | NULL      | Associate  | Loan     |
|    104 | Alex   | NULL      | Accountant | IT       |
|    105 | Victor | NULL      | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
4 rows in set (0.00 sec)

mysql> update Emplyees SET last_name = 'Sharma' WHERE emp_id = 101;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update Emplyees SET last_name = 'Thomas' WHERE emp_id = 103;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql>  update Emplyees SET last_name = 'Fernandes' WHERE emp_id = 104;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update Emplyees SET last_name = 'Das' WHERE emp_id = 105;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
4 rows in set (0.00 sec)

-----------------------------------------------------------------------------------------------------------------------------------------------------
CONCAT
-----------------------------------------------------------------------------------------------------------------------------------------------------

mysql> select CONCAT('Hey','BUDDY!');;
+------------------------+
| CONCAT('Hey','BUDDY!') |
+------------------------+
| HeyBUDDY!              |
+------------------------+
1 row in set (0.01 sec)

ERROR:
No query specified

mysql> select CONCAT('Hey','Buddy!','Hello');
+--------------------------------+
| CONCAT('Hey','Buddy!','Hello') |
+--------------------------------+
| HeyBuddy!Hello                 |
+--------------------------------+
1 row in set (0.00 sec)

mysql> select CONCAT ('Hey',' ','Buddy!');
+-----------------------------+
| CONCAT ('Hey',' ','Buddy!') |
+-----------------------------+
| Hey Buddy!                  |
+-----------------------------+
1 row in set (0.00 sec)

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
4 rows in set (0.00 sec)

mysql> select emp_id, CONCAT(name,' ',last_name) as FullName from emplyees;
+--------+----------------+
| emp_id | FullName       |
+--------+----------------+
|    101 | Raju Sharma    |
|    103 | Paul Thomas    |
|    104 | Alex Fernandes |
|    105 | Victor Das     |
+--------+----------------+
4 rows in set (0.00 sec)

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
4 rows in set (0.00 sec)


mysql> select emp_id,CONCAT(name,'@gamil.com') as NewName from emplyees;
+--------+------------------+
| emp_id | NewName          |
+--------+------------------+
|    101 | Raju@gamil.com   |
|    103 | Paul@gamil.com   |
|    104 | Alex@gamil.com   |
|    105 | Victor@gamil.com |
+--------+------------------+
4 rows in set (0.00 sec)

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
4 rows in set (0.00 sec)

--------------------------------------------------------------------------------------------------------------------------------------------
CONCAT_WS 
---------------------------------------------------------------------------------------------------------------------------------------------

mysql> select CONCAT_WS('-','Hi','Hello');
+-----------------------------+
| CONCAT_WS('-','Hi','Hello') |
+-----------------------------+
| Hi-Hello                    |
+-----------------------------+
1 row in set (0.01 sec)

mysql> select Concat_ws('-','hi','hello','how','are','u');
+---------------------------------------------+
| Concat_ws('-','hi','hello','how','are','u') |
+---------------------------------------------+
| hi-hello-how-are-u                          |
+---------------------------------------------+
1 row in set (0.00 sec)

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
4 rows in set (0.00 sec)


mysql> select CONCAT_WS(' : ',emp_id,name,last_name,desig,dept)
    -> from emplyees;
+---------------------------------------------------+
| CONCAT_WS(' : ',emp_id,name,last_name,desig,dept) |
+---------------------------------------------------+
| 101 : Raju : Sharma : Manager : Loan              |
| 103 : Paul : Thomas : Associate : Loan            |
| 104 : Alex : Fernandes : Accountant : IT          |
| 105 : Victor : Das : Associate : Deposite         |
+---------------------------------------------------+
4 rows in set (0.00 sec)

mysql>

-------------------------------------------------------------------------------------------------------------------------------------
SUBSTRING STR
----------------------------------------------------------------------------------------------------------------------------------
mysql> SELECT SUBSTRING('Hello Buddy', 1, 4);
+--------------------------------+
| SUBSTRING('Hello Buddy', 1, 4) |
+--------------------------------+
| Hell                           |
+--------------------------------+
1 row in set (0.00 sec)

mysql> SELECT SUBSTRING('Hey Buddy',5,9);
+----------------------------+
| SUBSTRING('Hey Buddy',5,9) |
+----------------------------+
| Buddy                      |
+----------------------------+
1 row in set (0.00 sec)

mysql> SELECT SUBSTRING('Hey Buddy',5);
+--------------------------+
| SUBSTRING('Hey Buddy',5) |
+--------------------------+
| Buddy                    |
+--------------------------+
1 row in set (0.00 sec)

mysql> SELECT SUBSTRING('Hey Buddy, watsup Raju',-4);
+----------------------------------------+
| SUBSTRING('Hey Buddy, watsup Raju',-4) |
+----------------------------------------+
| Raju                                   |
+----------------------------------------+
1 row in set (0.01 sec)

mysql> select * from emplyees
    -> ;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
4 rows in set (0.00 sec)

mysql> SELECT SUBSTRING(emp_id, 2, 3) AS emp_id,
    -> name from Emplyees;
+--------+--------+
| emp_id | name   |
+--------+--------+
| 01     | Raju   |
| 03     | Paul   |
| 04     | Alex   |
| 05     | Victor |
+--------+--------+
4 rows in set (0.00 sec)

mysql>
------------------------------------------------------------------------------------------------------------------------------------
