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

