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
REPLACR
-----------------------------------------------------------------------------------------------------------------------------------
mysql> SELECT REPLACE ('Hey Buddy','Hey','Hello');
+-------------------------------------+
| REPLACE ('Hey Buddy','Hey','Hello') |
+-------------------------------------+
| Hello Buddy                         |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT REPLACE ('ABCDPQR','PQR','XYZ');
+---------------------------------+
| REPLACE ('ABCDPQR','PQR','XYZ') |
+---------------------------------+
| ABCDXYZ                         |
+---------------------------------+
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

mysql> SELECT REPLACE(emp_id, 10, 10000)
    -> AS NewEmpIDS,
    -> name FROM emplyees;
+-----------+--------+
| NewEmpIDS | name   |
+-----------+--------+
| 100001    | Raju   |
| 100003    | Paul   |
| 100004    | Alex   |
| 100005    | Victor |
+-----------+--------+
4 rows in set (0.00 sec)

mysql> SELECT REPLACE(emp_id, 10, 'EMP')
    -> AS NewEmpIDS, name FROM emplyees;
+-----------+--------+
| NewEmpIDS | name   |
+-----------+--------+
| EMP1      | Raju   |
| EMP3      | Paul   |
| EMP4      | Alex   |
| EMP5      | Victor |
+-----------+--------+
4 rows in set (0.00 sec)
----------------------------------------------------------------------------------------------------------------------------------------
REVERSE STRING
----------------------------------------------------------------------------------------------------------------------------------------
mysql> SELECT REVERSE('HELLO');
+------------------+
| REVERSE('HELLO') |
+------------------+
| OLLEH            |
+------------------+
1 row in set (0.01 sec)

select * from emplyees' at line 1
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

mysql> SELECT REVERSE(name) AS rname
    -> from emplyees;
+--------+
| rname  |
+--------+
| ujaR   |
| luaP   |
| xelA   |
| rotciV |
+--------+
4 rows in set (0.00 sec)
###############################################################################################################################################
UPPER AND LOWER CASE
###############################################################################################################################################

mysql> select upper('abcdpqr');
+------------------+
| upper('abcdpqr') |
+------------------+
| ABCDPQR          |
+------------------+
1 row in set (0.01 sec)

mysql> select lower('ASDFGHJ');
+------------------+
| lower('ASDFGHJ') |
+------------------+
| asdfghj          |
+------------------+
1 row in set (0.00 sec)

mysql> select ucase('qwertyuiop');
+---------------------+
| ucase('qwertyuiop') |
+---------------------+
| QWERTYUIOP          |
+---------------------+
1 row in set (0.00 sec)

mysql> select lcase('ZXCVBNM');
+------------------+
| lcase('ZXCVBNM') |
+------------------+
| zxcvbnm          |
+------------------+
1 row in set (0.00 sec)

mysql> select emp_id,upper(name)
    -> from emplyees;
+--------+-------------+
| emp_id | upper(name) |
+--------+-------------+
|    101 | RAJU        |
|    103 | PAUL        |
|    104 | ALEX        |
|    105 | VICTOR      |
+--------+-------------+
4 rows in set (0.00 sec)

----------------------------------------------------------------------------------------------------------------------------------------------
CHAR_LENGTH
-------------------------------------------------------------------------------------------------------------------------------------------
mysql> select CHAR_LENGTH('Raju');
+---------------------+
| CHAR_LENGTH('Raju') |
+---------------------+
|                   4 |
+---------------------+
1 row in set (0.01 sec)

mysql> select CHAR_LENGTH('Raju Hello');
+---------------------------+
| CHAR_LENGTH('Raju Hello') |
+---------------------------+
|                        10 |
+---------------------------+
1 row in set (0.00 sec)

mysql> select name, CHAR_LENGTH(name) AS Length from emplyees;
+--------+--------+
| name   | Length |
+--------+--------+
| Raju   |      4 |
| Paul   |      4 |
| Alex   |      4 |
| Victor |      6 |
+--------+--------+
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

mysql> select * from emplyees
    -> WHERE CHAR_LENGTH(name)>5;
+--------+--------+-----------+-----------+----------+
| emp_id | name   | last_name | desig     | dept     |
+--------+--------+-----------+-----------+----------+
|    105 | Victor | Das       | Associate | Deposite |
+--------+--------+-----------+-----------+----------+
1 row in set (0.01 sec)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
LEFT RIGHT REPEAT TRIM INSERT
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> SELECT INSERT ('Hey wassup',5,0,'Raju ');
+-----------------------------------+
| INSERT ('Hey wassup',5,0,'Raju ') |
+-----------------------------------+
| Hey Raju wassup                   |
+-----------------------------------+
1 row in set (0.00 sec)

mysql> Select left('Hey Buddy Raju', 3);
+---------------------------+
| left('Hey Buddy Raju', 3) |
+---------------------------+
| Hey                       |
+---------------------------+
1 row in set (0.00 sec)

mysql> Select right('Hey Buddy Raju', 4);
+----------------------------+
| right('Hey Buddy Raju', 4) |
+----------------------------+
| Raju                       |
+----------------------------+
1 row in set (0.00 sec)

mysql> Select REPEAT('Hahahahaha ', 10);
+----------------------------------------------------------------------------------------------------------------+
| REPEAT('Hahahahaha ', 10)                                                                                      |
+----------------------------------------------------------------------------------------------------------------+
| Hahahahaha Hahahahaha Hahahahaha Hahahahaha Hahahahaha Hahahahaha Hahahahaha Hahahahaha Hahahahaha Hahahahaha  |
+----------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT TRIM('      SHRINIVAS                                                    ');
+-----------------------------------------------------------------------------+
| TRIM('      SHRINIVAS                                                    ') |
+-----------------------------------------------------------------------------+
| SHRINIVAS                                                                   |
+-----------------------------------------------------------------------------+
1 row in set (0.00 sec)

----------------------------------------------------------------------------------------------------------------------------------------------------------
EXERCISE 3
----------------------------------------------------------------------------------------------------------------------------------------------------------
QUESTION

+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+

Task 1:
101:Raju:Manager:Loan
Task2:
101:Raju Rastogi:Manager:Loan
Task3
101:Raju:MANAGER:Loan
Task4
L101 Raju
C102 Sham
-------------------------------------------------------------------------------------------------------------------------------------------------------------
ANSWER:->

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

mysql> select CONCAT_WS(':',emp_id,name,desig,dept) from emplyees;
+---------------------------------------+
| CONCAT_WS(':',emp_id,name,desig,dept) |
+---------------------------------------+
| 101:Raju:Manager:Loan                 |
| 103:Paul:Associate:Loan               |
| 104:Alex:Accountant:IT                |
| 105:Victor:Associate:Deposite         |
+---------------------------------------+
4 rows in set (0.00 sec)

mysql> select CONCAT_WS(':',emp_id,CONCAT(name,' ',last_name),desig,dept) from emplyees;
+-------------------------------------------------------------+
| CONCAT_WS(':',emp_id,CONCAT(name,' ',last_name),desig,dept) |
+-------------------------------------------------------------+
| 101:Raju Sharma:Manager:Loan                                |
| 103:Paul Thomas:Associate:Loan                              |
| 104:Alex Fernandes:Accountant:IT                            |
| 105:Victor Das:Associate:Deposite                           |
+-------------------------------------------------------------+
4 rows in set (0.00 sec)

mysql> select CONCAT_WS(':',emp_id,name,UPPER(desig),dept) from emplyees;
+----------------------------------------------+
| CONCAT_WS(':',emp_id,name,UPPER(desig),dept) |
+----------------------------------------------+
| 101:Raju:MANAGER:Loan                        |
| 103:Paul:ASSOCIATE:Loan                      |
| 104:Alex:ACCOUNTANT:IT                       |
| 105:Victor:ASSOCIATE:Deposite                |
+----------------------------------------------+
4 rows in set (0.00 sec)

mysql> SELECT emp_id,name from emplyees;
+--------+--------+
| emp_id | name   |
+--------+--------+
|    101 | Raju   |
|    103 | Paul   |
|    104 | Alex   |
|    105 | Victor |
+--------+--------+
4 rows in set (0.00 sec)

mysql> SELECT CONCAT(dept,emp_id),name from emplyees;
+---------------------+--------+
| CONCAT(dept,emp_id) | name   |
+---------------------+--------+
| Loan101             | Raju   |
| Loan103             | Paul   |
| IT104               | Alex   |
| Deposite105         | Victor |
+---------------------+--------+
4 rows in set (0.00 sec)

mysql> SELECT CONCAT(LEFT(dept, 1),emp_id),name from emplyees;
+------------------------------+--------+
| CONCAT(LEFT(dept, 1),emp_id) | name   |
+------------------------------+--------+
| L101                         | Raju   |
| L103                         | Paul   |
| I104                         | Alex   |
| D105                         | Victor |
+------------------------------+--------+
4 rows in set (0.00 sec)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
|    106 | Rick   | Watt      | Manager    | Account  |
+--------+--------+-----------+------------+----------+
6 rows in set (0.00 sec)
-------------------------------------------------------------------------------------------------------------------
INSERTING MORE VALUES
-------------------------------------------------------------------------------------------------------------------------------
mysql> INSERT INTO emplyees(emp_id,name,last_name,desig,dept)
    -> Values
    -> ('107','Alex','Watt','Lead','Cash'),
    -> ('108','John','Paul','Manager','Account'),
    -> ('109','Rick','Watt','Probation','Loan');
Query OK, 3 rows affected (0.03 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
|    106 | Rick   | Watt      | Manager    | Account  |
|    107 | Alex   | Watt      | Lead       | Cash     |
|    108 | John   | Paul      | Manager    | Account  |
|    109 | Rick   | Watt      | Probation  | Loan     |
+--------+--------+-----------+------------+----------+
9 rows in set (0.00 sec)
--------------------------------------------------------------------------------
What is DISTINCT
------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
|    106 | Rick   | Watt      | Manager    | Account  |
|    107 | Alex   | Watt      | Lead       | Cash     |
|    108 | John   | Paul      | Manager    | Account  |
|    109 | Rick   | Watt      | Probation  | Loan     |
+--------+--------+-----------+------------+----------+
9 rows in set (0.00 sec)

mysql> select dept from emplyees;
+----------+
| dept     |
+----------+
| Loan     |
| Cash     |
| Loan     |
| IT       |
| Deposite |
| Account  |
| Cash     |
| Account  |
| Loan     |
+----------+
9 rows in set (0.00 sec)

mysql> SELECT DISTINCT ^C
mysql> SELECT DISTINCT dept from emplyees;
+----------+
| dept     |
+----------+
| Loan     |
| Cash     |
| IT       |
| Deposite |
| Account  |
+----------+
5 rows in set (0.00 sec)

mysql> SELECT name,last_name from emplyees;
+--------+-----------+
| name   | last_name |
+--------+-----------+
| Raju   | Sharma    |
| Sham   | Mohan     |
| Paul   | Thomas    |
| Alex   | Fernandes |
| Victor | Das       |
| Rick   | Watt      |
| Alex   | Watt      |
| John   | Paul      |
| Rick   | Watt      |
+--------+-----------+
9 rows in set (0.00 sec)

mysql> SELECT DISTINCT name,last_name from emplyees;
+--------+-----------+
| name   | last_name |
+--------+-----------+
| Raju   | Sharma    |
| Sham   | Mohan     |
| Paul   | Thomas    |
| Alex   | Fernandes |
| Victor | Das       |
| Rick   | Watt      |
| Alex   | Watt      |
| John   | Paul      |
+--------+-----------+
8 rows in set (0.00 sec)

-------------------------------------------------------------------------------------------------------------------------------------
USE BY ORDER KEY
----------------------------------------------------------------------------------------------------------------------------------
mysql>  select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
|    106 | Rick   | Watt      | Manager    | Account  |
|    107 | Alex   | Watt      | Lead       | Cash     |
|    108 | John   | Paul      | Manager    | Account  |
|    109 | Rick   | Watt      | Probation  | Loan     |
+--------+--------+-----------+------------+----------+
9 rows in set (0.00 sec)

mysql>  select * from emplyees
    -> order by name;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    104 | Alex   | Fernandes | Accountant | IT       |
|    107 | Alex   | Watt      | Lead       | Cash     |
|    108 | John   | Paul      | Manager    | Account  |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    106 | Rick   | Watt      | Manager    | Account  |
|    109 | Rick   | Watt      | Probation  | Loan     |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    105 | Victor | Das       | Associate  | Deposite |
+--------+--------+-----------+------------+----------+
9 rows in set (0.01 sec)

mysql>  select * from emplyees
    -> order by name desc;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    105 | Victor | Das       | Associate  | Deposite |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    106 | Rick   | Watt      | Manager    | Account  |
|    109 | Rick   | Watt      | Probation  | Loan     |
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    108 | John   | Paul      | Manager    | Account  |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    107 | Alex   | Watt      | Lead       | Cash     |
+--------+--------+-----------+------------+----------+
9 rows in set (0.00 sec)

mysql>  select dept,name from emplyees;
+----------+--------+
| dept     | name   |
+----------+--------+
| Loan     | Raju   |
| Cash     | Sham   |
| Loan     | Paul   |
| IT       | Alex   |
| Deposite | Victor |
| Account  | Rick   |
| Cash     | Alex   |
| Account  | John   |
| Loan     | Rick   |
+----------+--------+
9 rows in set (0.00 sec)

mysql> select dept,name from emplyees
    -> order by dept,name;
+----------+--------+
| dept     | name   |
+----------+--------+
| Account  | John   |
| Account  | Rick   |
| Cash     | Alex   |
| Cash     | Sham   |
| Deposite | Victor |
| IT       | Alex   |
| Loan     | Paul   |
| Loan     | Raju   |
| Loan     | Rick   |
+----------+--------+
9 rows in set (0.00 sec)

-------------------------------------------------------------------------------------------------------------------------
USE OF LIKE KEYWORD
----------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
|    106 | Rick   | Watt      | Manager    | Account  |
|    107 | Alex   | Watt      | Lead       | Cash     |
|    108 | John   | Paul      | Manager    | Account  |
|    109 | Rick   | Watt      | Probation  | Loan     |
+--------+--------+-----------+------------+----------+
9 rows in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE desig LIKE "%Cash%";
+--------+------+-----------+---------+------+
| emp_id | name | last_name | desig   | dept |
+--------+------+-----------+---------+------+
|    102 | Sham | Mohan     | Cashier | Cash |
+--------+------+-----------+---------+------+
1 row in set (0.00 sec)

mysql> select * from emplyees
    -> where name LIKE "%____%";
+--------+--------+-----------+------------+----------+
| emp_id | name   | last_name | desig      | dept     |
+--------+--------+-----------+------------+----------+
|    101 | Raju   | Sharma    | Manager    | Loan     |
|    102 | Sham   | Mohan     | Cashier    | Cash     |
|    103 | Paul   | Thomas    | Associate  | Loan     |
|    104 | Alex   | Fernandes | Accountant | IT       |
|    105 | Victor | Das       | Associate  | Deposite |
|    106 | Rick   | Watt      | Manager    | Account  |
|    107 | Alex   | Watt      | Lead       | Cash     |
|    108 | John   | Paul      | Manager    | Account  |
|    109 | Rick   | Watt      | Probation  | Loan     |
+--------+--------+-----------+------------+----------+
9 rows in set (0.00 sec)

mysql> select * from emplyees
    ->  where name LIKE "%r___%";
+--------+------+-----------+-----------+---------+
| emp_id | name | last_name | desig     | dept    |
+--------+------+-----------+-----------+---------+
|    101 | Raju | Sharma    | Manager   | Loan    |
|    106 | Rick | Watt      | Manager   | Account |
|    109 | Rick | Watt      | Probation | Loan    |
+--------+------+-----------+-----------+---------+
3 rows in set (0.00 sec)
------------------------------------------------------------------------------------------------------------------
ADDING SALARY COLUMN AND CHANGING SALARY
--------------------------------------------------------------------------------------------------------------
mysql> ALTER TABLE emplyees
    -> ADD COLUMN
    -> Salary INT NOT NULL
    -> DEFAULT 25000;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  25000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  25000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  25000 |
|    105 | Victor | Das       | Associate  | Deposite |  25000 |
|    106 | Rick   | Watt      | Manager    | Account  |  25000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  25000 |
|    108 | John   | Paul      | Manager    | Account  |  25000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  25000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> update emplyees
    -> SET Salary=37000
    -> Where name='Raju';
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  25000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  25000 |
|    105 | Victor | Das       | Associate  | Deposite |  25000 |
|    106 | Rick   | Watt      | Manager    | Account  |  25000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  25000 |
|    108 | John   | Paul      | Manager    | Account  |  25000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  25000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> UPDATE emplyees SET Salary = 32000 WHERE name = 'Paul';
Query OK, 1 row affected (0.04 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE emplyees SET Salary = 28000 WHERE name = 'Alex';
Query OK, 2 rows affected (0.02 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> UPDATE emplyees SET Salary = 28000 WHERE name = 'Alex';
Query OK, 0 rows affected (0.00 sec)
Rows matched: 2  Changed: 0  Warnings: 0

mysql> UPDATE emplyees SET Salary = 30000 WHERE name = 'Rick';
Query OK, 2 rows affected (0.02 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> UPDATE emplyees SET Salary = 31000 WHERE name = 'John';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE emplyees SET Salary = 26000 WHERE name = 'Victor';
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)
------------------------------------------------------------------------------------------------------------------------------------------
LIMIT
----------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees LIMIT 5;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
+--------+--------+-----------+------------+----------+--------+
5 rows in set (0.00 sec)

mysql> select * from emplyees LIMIT 3, 2;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
+--------+--------+-----------+------------+----------+--------+
2 rows in set (0.00 sec)

mysql> select * from emplyees order by Salary DESC;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees order by Salary DESC
    -> LIMIT 1;
+--------+------+-----------+---------+------+--------+
| emp_id | name | last_name | desig   | dept | Salary |
+--------+------+-----------+---------+------+--------+
|    101 | Raju | Sharma    | Manager | Loan |  37000 |
+--------+------+-----------+---------+------+--------+
1 row in set (0.00 sec)

----------------------------------------------------------------------------------------------------------------------------------------------
COUNT()
----------------------------------------------------------------------------------------------------------------------------------------------

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select COUNT(*) from emplyees;
+----------+
| COUNT(*) |
+----------+
|        9 |
+----------+
1 row in set (0.02 sec)

mysql>  select COUNT(name) from emplyees;
+-------------+
| COUNT(name) |
+-------------+
|           9 |
+-------------+
1 row in set (0.02 sec)

mysql>  select COUNT(dept) from emplyees;
+-------------+
| COUNT(dept) |
+-------------+
|           9 |
+-------------+
1 row in set (0.00 sec)

mysql>  select COUNT(DISTINCT dept) from emplyees;
+----------------------+
| COUNT(DISTINCT dept) |
+----------------------+
|                    5 |
+----------------------+
1 row in set (0.01 sec)

mysql>  select COUNT(emp_id) from emplyees
    -> WHERE desig = "Manager";
+---------------+
| COUNT(emp_id) |
+---------------+
|             3 |
+---------------+
1 row in set (0.01 sec)

mysql>  select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

----------------------------------------------------------------------------------------------------------------------------------------
Exercise - 4
DISTINCT, ORDER BY, LIKE and LIMIT
---------------------------------------------------------------------------------------------------------------------------------------
QUESTION
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+

1: Find Different type of departments in database?
2: Display records with High-low salary
3: How to see only top 3 records from a table?
4: Show records where first name start with letter 'A'
5: Show records where length of the lname is 4 characters
----------------------------------------------------------------------------------------------------------------------------------
ANSWER
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select DISTINCT dept from emplyees;
+----------+
| dept     |
+----------+
| Loan     |
| Cash     |
| IT       |
| Deposite |
| Account  |
+----------+
5 rows in set (0.00 sec)

mysql> select * from emplyees
    -> order by Salary DESC;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees LIMIT 3;
+--------+------+-----------+-----------+------+--------+
| emp_id | name | last_name | desig     | dept | Salary |
+--------+------+-----------+-----------+------+--------+
|    101 | Raju | Sharma    | Manager   | Loan |  37000 |
|    102 | Sham | Mohan     | Cashier   | Cash |  25000 |
|    103 | Paul | Thomas    | Associate | Loan |  32000 |
+--------+------+-----------+-----------+------+--------+
3 rows in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE name LIKE "A%"; or "A___"
+--------+------+-----------+------------+------+--------+
| emp_id | name | last_name | desig      | dept | Salary |
+--------+------+-----------+------------+------+--------+
|    104 | Alex | Fernandes | Accountant | IT   |  28000 |
|    107 | Alex | Watt      | Lead       | Cash |  28000 |
+--------+------+-----------+------------+------+--------+
2 rows in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE last_name LIKE "____";
+--------+------+-----------+-----------+---------+--------+
| emp_id | name | last_name | desig     | dept    | Salary |
+--------+------+-----------+-----------+---------+--------+
|    106 | Rick | Watt      | Manager   | Account |  30000 |
|    107 | Alex | Watt      | Lead      | Cash    |  28000 |
|    108 | John | Paul      | Manager   | Account |  31000 |
|    109 | Rick | Watt      | Probation | Loan    |  30000 |
+--------+------+-----------+-----------+---------+--------+
4 rows in set (0.00 sec)

---------------------------------------------------------------------------------------------------------------------------------------------------
GROUP BY
--------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select dept from emplyees group by dept;
+----------+
| dept     |
+----------+
| Loan     |
| Cash     |
| IT       |
| Deposite |
| Account  |
+----------+
5 rows in set (0.00 sec)

mysql> select dept,COUNT(emp_id) from emplyees group by dept;
+----------+---------------+
| dept     | COUNT(emp_id) |
+----------+---------------+
| Loan     |             3 |
| Cash     |             2 |
| IT       |             1 |
| Deposite |             1 |
| Account  |             2 |
+----------+---------------+
5 rows in set (0.01 sec)

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select desig from emplyees group by desig;
+------------+
| desig      |
+------------+
| Manager    |
| Cashier    |
| Associate  |
| Accountant |
| Lead       |
| Probation  |
+------------+
6 rows in set (0.00 sec)

mysql>
mysql> select desig,COUNT(emp_id) from emplyees group by desig;
+------------+---------------+
| desig      | COUNT(emp_id) |
+------------+---------------+
| Manager    |             3 |
| Cashier    |             1 |
| Associate  |             2 |
| Accountant |             1 |
| Lead       |             1 |
| Probation  |             1 |
+------------+---------------+
6 rows in set (0.00 sec)
-------------------------------------------------------------------------------------------------
FUNCTION MIN & MAX
---------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select MAX(salary) from emplyees;
+-------------+
| MAX(salary) |
+-------------+
|       37000 |
+-------------+
1 row in set (0.01 sec)

mysql> select MIN(salary) from emplyees;
+-------------+
| MIN(salary) |
+-------------+
|       25000 |
+-------------+
1 row in set (0.01 sec)

mysql> Select MAX(name) from emplyees;
+-----------+
| MAX(name) |
+-----------+
| Victor    |
+-----------+
1 row in set (0.00 sec)

mysql> Select MIN(name) from emplyees;
+-----------+
| MIN(name) |
+-----------+
| Alex      |
+-----------+
1 row in set (0.00 sec)

----------------------------------------------------------------------------------------------------------
SUB QUERIES MAX MIN
----------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select emp_id,name,salary from emplyees
    -> WHERE
    -> Salary = (Select MAX(Salary) from emplyees);
+--------+------+--------+
| emp_id | name | salary |
+--------+------+--------+
|    101 | Raju |  37000 |
+--------+------+--------+
1 row in set (0.01 sec)
--------------------------------------------------------------------------------------------------------------
SUM & AVG Function
--------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select sum(Salary) from emplyees;
+-------------+
| sum(Salary) |
+-------------+
|      267000 |
+-------------+
1 row in set (0.01 sec)

mysql> select AVG(Salary) from emplyees;
+-------------+
| AVG(Salary) |
+-------------+
|  29666.6667 |
+-------------+
1 row in set (0.01 sec)

mysql> select dept,sum(Salary) from emplyees
    -> group by dept;
+----------+-------------+
| dept     | sum(Salary) |
+----------+-------------+
| Loan     |       99000 |
| Cash     |       53000 |
| IT       |       28000 |
| Deposite |       26000 |
| Account  |       61000 |
+----------+-------------+
5 rows in set (0.00 sec)

mysql> select dept,COUNT(emp_id),sum(Salary) from emplyees
    -> group by dept;
+----------+---------------+-------------+
| dept     | COUNT(emp_id) | sum(Salary) |
+----------+---------------+-------------+
| Loan     |             3 |       99000 |
| Cash     |             2 |       53000 |
| IT       |             1 |       28000 |
| Deposite |             1 |       26000 |
| Account  |             2 |       61000 |
+----------+---------------+-------------+
5 rows in set (0.00 sec)
---------------------------------------------------------------------------------------------------------------------
Exercise - 4
DISTINCT, ORDER BY, LIKE and LIMIT
------------------------------------------------------------------------------------------------------------------
QUESTIONS 
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+

1: Find Different type of departments in database?
2: Display records with High-low salary
3: How to see only top 3 records from a table?
4: Show records where first name start with letter 'A'
5: Show records where length of the lname is 4 characters
-----------------------------------------------------------------------------------------------------------------
ANSWER
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select COUNT(emp_id) from emplyees;
+---------------+
| COUNT(emp_id) |
+---------------+
|             9 |
+---------------+
1 row in set (0.00 sec)

mysql> select dept,COUNT(emp_id) from emplyees
    -> group by dept;
+----------+---------------+
| dept     | COUNT(emp_id) |
+----------+---------------+
| Loan     |             3 |
| Cash     |             2 |
| IT       |             1 |
| Deposite |             1 |
| Account  |             2 |
+----------+---------------+
5 rows in set (0.00 sec)

mysql> select MIN(salary) from emplyees;
+-------------+
| MIN(salary) |
+-------------+
|       25000 |
+-------------+
1 row in set (0.00 sec)

mysql> select MAX(salary) from emplyees;
+-------------+
| MAX(salary) |
+-------------+
|       37000 |
+-------------+
1 row in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE salary=(select MAX(salary) from emplyees);
+--------+------+-----------+---------+------+--------+
| emp_id | name | last_name | desig   | dept | Salary |
+--------+------+-----------+---------+------+--------+
|    101 | Raju | Sharma    | Manager | Loan |  37000 |
+--------+------+-----------+---------+------+--------+
1 row in set (0.00 sec)

mysql>  select * from emplyees
    -> WHERE dept = "Loan";
+--------+------+-----------+-----------+------+--------+
| emp_id | name | last_name | desig     | dept | Salary |
+--------+------+-----------+-----------+------+--------+
|    101 | Raju | Sharma    | Manager   | Loan |  37000 |
|    103 | Paul | Thomas    | Associate | Loan |  32000 |
|    109 | Rick | Watt      | Probation | Loan |  30000 |
+--------+------+-----------+-----------+------+--------+
3 rows in set (0.00 sec)

mysql>  select SUM(Salary) from emplyees
    -> WHERE dept = "Loan";
+-------------+
| SUM(Salary) |
+-------------+
|       99000 |
+-------------+
1 row in set (0.00 sec)

mysql> select dept,AVG(Salary) from emplyees
    -> group by dept;
+----------+-------------+
| dept     | AVG(Salary) |
+----------+-------------+
| Loan     |  33000.0000 |
| Cash     |  26500.0000 |
| IT       |  28000.0000 |
| Deposite |  26000.0000 |
| Account  |  30500.0000 |
+----------+-------------+
5 rows in set (0.01 sec)
-------------------------------------------------------------------------------------------------------------------------------------------------------
DATA TYPE DECIMAL
-------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> CREATE TABLE NUM(Price DECIMAL(5,2));
Query OK, 0 rows affected (0.06 sec)

mysql> desc num;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| Price | decimal(5,2) | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
1 row in set (0.00 sec)

mysql> INSERT INTO NUM VALUES(155.78);
Query OK, 1 row affected (0.01 sec)

mysql> select * from num;
+--------+
| Price  |
+--------+
| 155.78 |
+--------+
1 row in set (0.00 sec)

mysql> INSERT INTO NUM VALUES(1557.78);
ERROR 1264 (22003): Out of range value for column 'Price' at row 1
mysql> INSERT INTO NUM VALUES(15.78);
Query OK, 1 row affected (0.03 sec)

mysql> select * from num;
+--------+
| Price  |
+--------+
| 155.78 |
|  15.78 |
+--------+
2 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
DATA TYPES FLOAT & INT
----------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> create table num2
    -> (f Float, d Double);
Query OK, 0 rows affected (0.04 sec)

mysql> insert into num2 values(123.456, 123.456);
Query OK, 1 row affected (0.02 sec)

mysql> select * from num2;
+---------+---------+
| f       | d       |
+---------+---------+
| 123.456 | 123.456 |
+---------+---------+
1 row in set (0.00 sec)

mysql> insert into num2 values(123.123456789, 123.123456789);
Query OK, 1 row affected (0.01 sec)

mysql> select * from num2;
+---------+---------------+
| f       | d             |
+---------+---------------+
| 123.456 |       123.456 |
| 123.123 | 123.123456789 |
+---------+---------------+
2 rows in set (0.00 sec)

mysql> insert into num2 values(123.123456789, 123.12345678900987654321);
Query OK, 1 row affected (0.01 sec)

mysql>  select * from num2;
+---------+--------------------+
| f       | d                  |
+---------+--------------------+
| 123.456 |            123.456 |
| 123.123 |      123.123456789 |
| 123.123 | 123.12345678900988 |
+---------+--------------------+
3 rows in set (0.00 sec)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
DATA TYPE DATE AND TIME
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> create table person
    -> (jd Date,
    -> jt Time,
    -> jdt DateTime);
Query OK, 0 rows affected (0.06 sec)

mysql> desc person;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| jd    | date     | YES  |     | NULL    |       |
| jt    | time     | YES  |     | NULL    |       |
| jdt   | datetime | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> INSERT INTO person
    -> Values('2025:04:17','20:08:45','2025-06-17 07:32:54');
Query OK, 1 row affected, 1 warning (0.02 sec)

mysql> select * from person;
+------------+----------+---------------------+
| jd         | jt       | jdt                 |
+------------+----------+---------------------+
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
+------------+----------+---------------------+
1 row in set (0.00 sec)

mysql> INsert into person
    -> Values('2025-04-17','20:08:45','2025-06-17 07:32:54');
Query OK, 1 row affected (0.01 sec)

mysql> select * from person;
+------------+----------+---------------------+
| jd         | jt       | jdt                 |
+------------+----------+---------------------+
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
+------------+----------+---------------------+
2 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------------
FUNCTIONS FOR DATE AND TIME - CURDATE(),CURTIME(),NOW()
----------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> SELECT CURDATE();
+------------+
| CURDATE()  |
+------------+
| 2025-06-18 |
+------------+
1 row in set (0.01 sec)

mysql> SELECT CURTIME();
+-----------+
| CURTIME() |
+-----------+
| 07:36:01  |
+-----------+
1 row in set (0.00 sec)

mysql> SELECT NOW();
+---------------------+
| NOW()               |
+---------------------+
| 2025-06-18 07:36:14 |
+---------------------+
1 row in set (0.01 sec)

mysql> INSERT INTO PERSON VALUES(CURDATE(),CURTIME(),NOW());
Query OK, 1 row affected (0.01 sec)

mysql> select * from person;
+------------+----------+---------------------+
| jd         | jt       | jdt                 |
+------------+----------+---------------------+
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-06-18 | 07:37:11 | 2025-06-18 07:37:11 |
+------------+----------+---------------------+
3 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------
DATE TIME FUNCTIONS
--------------------------------------------------------------------------------------------------------------------------------------
mysql> select dayname('2025-05-18');
+-----------------------+
| dayname('2025-05-18') |
+-----------------------+
| Sunday                |
+-----------------------+
1 row in set (0.01 sec)

mysql> select dayname(CURDATE());
+--------------------+
| dayname(CURDATE()) |
+--------------------+
| Wednesday          |
+--------------------+
1 row in set (0.00 sec)

mysql> SELECT DAYOFMONTH(CURDATE());
+-----------------------+
| DAYOFMONTH(CURDATE()) |
+-----------------------+
|                    18 |
+-----------------------+
1 row in set (0.00 sec)

mysql> SELECT DAYOFWEEK(CURDATE());
+----------------------+
| DAYOFWEEK(CURDATE()) |
+----------------------+
|                    4 |
+----------------------+
1 row in set (0.01 sec)

mysql> select monthname('2025-04-28');
+-------------------------+
| monthname('2025-04-28') |
+-------------------------+
| April                   |
+-------------------------+
1 row in set (0.00 sec)

mysql> select * from person;
+------------+----------+---------------------+
| jd         | jt       | jdt                 |
+------------+----------+---------------------+
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-06-18 | 07:37:11 | 2025-06-18 07:37:11 |
+------------+----------+---------------------+
3 rows in set (0.00 sec)

mysql> select jd, monthname(jd) from person;
+------------+---------------+
| jd         | monthname(jd) |
+------------+---------------+
| 2025-04-17 | April         |
| 2025-04-17 | April         |
| 2025-06-18 | June          |
+------------+---------------+
3 rows in set (0.00 sec)

mysql> select jd, YEAR(jd) from person;
+------------+----------+
| jd         | YEAR(jd) |
+------------+----------+
| 2025-04-17 |     2025 |
| 2025-04-17 |     2025 |
| 2025-06-18 |     2025 |
+------------+----------+
3 rows in set (0.01 sec)

mysql> select jd, DAYNAME(jd) from person;
+------------+-------------+
| jd         | DAYNAME(jd) |
+------------+-------------+
| 2025-04-17 | Thursday    |
| 2025-04-17 | Thursday    |
| 2025-06-18 | Wednesday   |
+------------+-------------+
3 rows in set (0.00 sec)

mysql> select jd, HOUR(jt) from person;
+------------+----------+
| jd         | HOUR(jt) |
+------------+----------+
| 2025-04-17 |       20 |
| 2025-04-17 |       20 |
| 2025-06-18 |        7 |
+------------+----------+
3 rows in set (0.00 sec)

mysql> select jd, MINUTE(jt) from person;
+------------+------------+
| jd         | MINUTE(jt) |
+------------+------------+
| 2025-04-17 |          8 |
| 2025-04-17 |          8 |
| 2025-06-18 |         37 |
+------------+------------+
3 rows in set (0.00 sec)
------------------------------------------------------------------------------------------------------------------------------------
DATE FORMATTING
------------------------------------------------------------------------------------------------------------------------------
mysql> select now();
+---------------------+
| now()               |
+---------------------+
| 2025-06-18 07:51:04 |
+---------------------+
1 row in set (0.00 sec)

mysql> select DATE_FORMAT(now(),'%d/%m/%y');
+-------------------------------+
| DATE_FORMAT(now(),'%d/%m/%y') |
+-------------------------------+
| 18/06/25                      |
+-------------------------------+
1 row in set (0.01 sec)

mysql> select DATE_FORMAT(now(),'%d');
+-------------------------+
| DATE_FORMAT(now(),'%d') |
+-------------------------+
| 18                      |
+-------------------------+
1 row in set (0.00 sec)

mysql> select DATE_FORMAT(now(),'%D %a');
+----------------------------+
| DATE_FORMAT(now(),'%D %a') |
+----------------------------+
| 18th Wed                   |
+----------------------------+
1 row in set (0.00 sec)

mysql> select DATE_FORMAT(now(),'%D %a at %k');
+----------------------------------+
| DATE_FORMAT(now(),'%D %a at %k') |
+----------------------------------+
| 18th Wed at 7                    |
+----------------------------------+
1 row in set (0.00 sec)

mysql> select * from person;
+------------+----------+---------------------+
| jd         | jt       | jdt                 |
+------------+----------+---------------------+
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-06-18 | 07:37:11 | 2025-06-18 07:37:11 |
+------------+----------+---------------------+
3 rows in set (0.00 sec)
mysql> select jdt, DATE_FORMAT(jdt, '%D %a at %k') from person;
+---------------------+---------------------------------+
| jdt                 | DATE_FORMAT(jdt, '%D %a at %k') |
+---------------------+---------------------------------+
| 2025-06-17 07:32:54 | 17th Tue at 7                   |
| 2025-06-17 07:32:54 | 17th Tue at 7                   |
| 2025-06-18 07:37:11 | 18th Wed at 7                   |
+---------------------+---------------------------------+
3 rows in set (0.00 sec)
----------------------------------------------------------------------------------------------------------------------------------------
DATE DIFF
----------------------------------------------------------------------------------------------------------------------------------------
mysql> select DateDiff('2025-05-18','2025-06-18');
+-------------------------------------+
| DateDiff('2025-05-18','2025-06-18') |
+-------------------------------------+
|                                 -31 |
+-------------------------------------+
1 row in set (0.01 sec)

mysql> select DateDiff('2024-06-01','2025-06-18');
+-------------------------------------+
| DateDiff('2024-06-01','2025-06-18') |
+-------------------------------------+
|                                -382 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-06-18','2025-11-18');
+-------------------------------------+
| DateDiff('2025-06-18','2025-11-18') |
+-------------------------------------+
|                                -153 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-05-18','2024-06-18');
+-------------------------------------+
| DateDiff('2025-05-18','2024-06-18') |
+-------------------------------------+
|                                 334 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-06-01','2024-05-20');
+-------------------------------------+
| DateDiff('2025-06-01','2024-05-20') |
+-------------------------------------+
|                                 377 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-06-18','2024-06-01');
+-------------------------------------+
| DateDiff('2025-06-18','2024-06-01') |
+-------------------------------------+
|                                 382 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-05-18','2025-05-18');
+-------------------------------------+
| DateDiff('2025-05-18','2025-05-18') |
+-------------------------------------+
|                                   0 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-05-18','2024-06-01');
+-------------------------------------+
| DateDiff('2025-05-18','2024-06-01') |
+-------------------------------------+
|                                 351 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-05-18','2024-04-22');
+-------------------------------------+
| DateDiff('2025-05-18','2024-04-22') |
+-------------------------------------+
|                                 391 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-04-22','2024-06-01');
+-------------------------------------+
| DateDiff('2025-04-22','2024-06-01') |
+-------------------------------------+
|                                 325 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-05-18','2025-04-22');
+-------------------------------------+
| DateDiff('2025-05-18','2025-04-22') |
+-------------------------------------+
|                                  26 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select DateDiff('2025-06-18','2025-04-22');
+-------------------------------------+
| DateDiff('2025-06-18','2025-04-22') |
+-------------------------------------+
|                                  57 |
+-------------------------------------+
1 row in set (0.00 sec)

mysql> select now();
+---------------------+
| now()               |
+---------------------+
| 2025-06-18 08:10:14 |
+---------------------+
1 row in set (0.00 sec)

mysql> select DATE_ADD(NOW(), INTERVAL 1 YEAR);
+----------------------------------+
| DATE_ADD(NOW(), INTERVAL 1 YEAR) |
+----------------------------------+
| 2026-06-18 08:10:54              |
+----------------------------------+
1 row in set (0.00 sec)

mysql> select DATE_ADD(2025-04-22, INTERVAL 1 YEAR);
+---------------------------------------+
| DATE_ADD(2025-04-22, INTERVAL 1 YEAR) |
+---------------------------------------+
| NULL                                  |
+---------------------------------------+
1 row in set, 1 warning (0.01 sec)

mysql> select DATE_ADD('2025-04-22', INTERVAL 1 YEAR);
+-----------------------------------------+
| DATE_ADD('2025-04-22', INTERVAL 1 YEAR) |
+-----------------------------------------+
| 2026-04-22                              |
+-----------------------------------------+
1 row in set (0.00 sec)

mysql> select DATE_ADD('2025-04-22', INTERVAL 6 MONTH);
+------------------------------------------+
| DATE_ADD('2025-04-22', INTERVAL 6 MONTH) |
+------------------------------------------+
| 2025-10-22                               |
+------------------------------------------+
1 row in set (0.01 sec)

mysql> select DATE_SUB('2025-04-22', INTERVAL 6 DAY);
+----------------------------------------+
| DATE_SUB('2025-04-22', INTERVAL 6 DAY) |
+----------------------------------------+
| 2025-04-16                             |
+----------------------------------------+
1 row in set (0.00 sec)

mysql> select DATE_SUB('2025-06-22', INTERVAL 1 MONTH);
+------------------------------------------+
| DATE_SUB('2025-06-22', INTERVAL 1 MONTH) |
+------------------------------------------+
| 2025-05-22                               |
+------------------------------------------+
1 row in set (0.00 sec)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
TIMEDIFF
------------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select TIMEDIFF('22:00:00','08:18:59');
+---------------------------------+
| TIMEDIFF('22:00:00','08:18:59') |
+---------------------------------+
| 13:41:01                        |
+---------------------------------+
1 row in set (0.01 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
DEFAULT & ON UPDATE TIMESTAMP
---------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> CREATE TABLE BLOGS(
    -> BLOG VARCHAR(50),
    -> ct DATETIME DEFAULT CURRENT_TIMESTAMP,
    -> ut DATETIME ON UPDATE CURRENT_TIMESTAMP
    -> );
Query OK, 0 rows affected (0.06 sec)

mysql> DESC BLOGS;
+-------+-------------+------+-----+-------------------+-----------------------------+
| Field | Type        | Null | Key | Default           | Extra                       |
+-------+-------------+------+-----+-------------------+-----------------------------+
| BLOG  | varchar(50) | YES  |     | NULL              |                             |
| ct    | datetime    | YES  |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED           |
| ut    | datetime    | YES  |     | NULL              | on update CURRENT_TIMESTAMP |
+-------+-------------+------+-----+-------------------+-----------------------------+
3 rows in set (0.02 sec)

mysql> INSERT INTO BLOGS(BLOG)
    -> VALUES('This is my first blog');
Query OK, 1 row affected (0.02 sec)

mysql> select * from blogs;
+-----------------------+---------------------+------+
| BLOG                  | ct                  | ut   |
+-----------------------+---------------------+------+
| This is my first blog | 2025-06-18 08:22:43 | NULL |
+-----------------------+---------------------+------+
1 row in set (0.00 sec)

mysql> update blogs
    -> set blog='This is my first blog from india';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from blogs;
+----------------------------------+---------------------+---------------------+
| BLOG                             | ct                  | ut                  |
+----------------------------------+---------------------+---------------------+
| This is my first blog from india | 2025-06-18 08:22:43 | 2025-06-18 08:26:04 |
+----------------------------------+---------------------+---------------------+
1 row in set (0.00 sec)

mysql> update blogs
    -> set blog='This is my first blog from US';
Query OK, 1 row affected (0.03 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from blogs;
+-------------------------------+---------------------+---------------------+
| BLOG                          | ct                  | ut                  |
+-------------------------------+---------------------+---------------------+
| This is my first blog from US | 2025-06-18 08:22:43 | 2025-06-18 08:26:42 |
+-------------------------------+---------------------+---------------------+
1 row in set (0.00 sec)
---------------------------------------------------------------------------------------------------------------------------------
Exercise - 6
----------------------------------------------------------------------------------------------------------------------------------
-> Print the current time (HH:MM:SS)
-> Print the current date (yyyy-mm-dd)
-> Print current day of the week (Monday, Tuesday...)
-> What is the use case of CHAR datatype?
-> Which datatype can be used to store value 123.456?
-> Display date in format
            *dd:mm:yyyy
            *April 22nd at 22:00:00

---------------------------------------------------------------------------------------------------------------------------------
SOLUTION
---------------------------------------------------------------------------------------------------------------------------------
mysql> SELECT CURTIME();
+-----------+
| CURTIME() |
+-----------+
| 08:33:20  |
+-----------+
1 row in set (0.00 sec)

mysql> SELECT CURDATE();
+------------+
| CURDATE()  |
+------------+
| 2025-06-18 |
+------------+
1 row in set (0.00 sec)

mysql> SELECT DAYNAME(NOW());
+----------------+
| DAYNAME(NOW()) |
+----------------+
| Wednesday      |
+----------------+
1 row in set (0.00 sec)

mysql> IF WE WANT TO STORE A FIXED LENGTH VALUE AS SAME FOREVER
    -> EG -> COUNTRY CODE;

mysql> DECIANL DATATYPE, FLOAT OR DOUBLE;

mysql> SELECT DATE_FORMAT(NOW(),'%d');
+-------------------------+
| DATE_FORMAT(NOW(),'%d') |
+-------------------------+
| 18                      |
+-------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(NOW(),'%d:%m');
+----------------------------+
| DATE_FORMAT(NOW(),'%d:%m') |
+----------------------------+
| 18:06                      |
+----------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(NOW(),'%d:%m:%y');
+-------------------------------+
| DATE_FORMAT(NOW(),'%d:%m:%y') |
+-------------------------------+
| 18:06:25                      |
+-------------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(NOW(),'%d,%m,%M');
+-------------------------------+
| DATE_FORMAT(NOW(),'%d,%m,%M') |
+-------------------------------+
| 18,06,June                    |
+-------------------------------+
1 row in set (0.00 sec)

mysql>
mysql> SELECT DATE_FORMAT(NOW(),'%M');
+-------------------------+
| DATE_FORMAT(NOW(),'%M') |
+-------------------------+
| June                    |
+-------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(NOW(),'%M %D');
+----------------------------+
| DATE_FORMAT(NOW(),'%M %D') |
+----------------------------+
| June 18th                  |
+----------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(NOW(),'%M %D at %T');
+----------------------------------+
| DATE_FORMAT(NOW(),'%M %D at %T') |
+----------------------------------+
| June 18th at 08:39:35            |
+----------------------------------+
1 row in set (0.00 sec)
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RELATIONAL OPERATORS
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE Salary = 37000;
+--------+------+-----------+---------+------+--------+
| emp_id | name | last_name | desig   | dept | Salary |
+--------+------+-----------+---------+------+--------+
|    101 | Raju | Sharma    | Manager | Loan |  37000 |
+--------+------+-----------+---------+------+--------+
1 row in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE Salary > 32000;
+--------+------+-----------+---------+------+--------+
| emp_id | name | last_name | desig   | dept | Salary |
+--------+------+-----------+---------+------+--------+
|    101 | Raju | Sharma    | Manager | Loan |  37000 |
+--------+------+-----------+---------+------+--------+
1 row in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE Salary < 32000;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
7 rows in set (0.00 sec)

mysql> select * from emplyees WHERE Salary <= 32000;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
8 rows in set (0.00 sec)

mysql> select * from emplyees WHERE Salary >= 32000;
+--------+------+-----------+-----------+------+--------+
| emp_id | name | last_name | desig     | dept | Salary |
+--------+------+-----------+-----------+------+--------+
|    101 | Raju | Sharma    | Manager   | Loan |  37000 |
|    103 | Paul | Thomas    | Associate | Loan |  32000 |
+--------+------+-----------+-----------+------+--------+
2 rows in set (0.00 sec)

mysql> select * from emplyees WHERE Salary != 37000;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
8 rows in set (0.00 sec)
---------------------------------------------------------------------------------------------------------------------------------------------------
LOGICAL OPERATORS -  AND - WHEN BOTH THE CONDITIONS ARE TRUE
--------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+

mysql> select * from emplyees WHERE Salary = 25000 AND dept='Cash';
+--------+------+-----------+---------+------+--------+
| emp_id | name | last_name | desig   | dept | Salary |
+--------+------+-----------+---------+------+--------+
|    102 | Sham | Mohan     | Cashier | Cash |  25000 |
+--------+------+-----------+---------+------+--------+

mysql> select * from emplyees WHERE Salary = 28000 AND dept='IT';
+--------+------+-----------+------------+------+--------+
| emp_id | name | last_name | desig      | dept | Salary |
+--------+------+-----------+------------+------+--------+
|    104 | Alex | Fernandes | Accountant | IT   |  28000 |
+--------+------+-----------+------------+------+--------+
1 row in set (0.00 sec)
-------------------------------------------------------------------------------------------------------------------------------
LOGICAL OPERATORS -  OR - WHEN EITHER OF THE CONDITIONS IS TRUE
-------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees WHERE Salary = 28000 OR dept='Loan';
+--------+------+-----------+------------+------+--------+
| emp_id | name | last_name | desig      | dept | Salary |
+--------+------+-----------+------------+------+--------+
|    101 | Raju | Sharma    | Manager    | Loan |  37000 |
|    103 | Paul | Thomas    | Associate  | Loan |  32000 |
|    104 | Alex | Fernandes | Accountant | IT   |  28000 |
|    107 | Alex | Watt      | Lead       | Cash |  28000 |
|    109 | Rick | Watt      | Probation  | Loan |  30000 |
+--------+------+-----------+------------+------+--------+
5 rows in set (0.00 sec)

mysql> select * from emplyees WHERE Salary=28000 OR Salary=37000 OR Salary=30000;
+--------+------+-----------+------------+---------+--------+
| emp_id | name | last_name | desig      | dept    | Salary |
+--------+------+-----------+------------+---------+--------+
|    101 | Raju | Sharma    | Manager    | Loan    |  37000 |
|    104 | Alex | Fernandes | Accountant | IT      |  28000 |
|    106 | Rick | Watt      | Manager    | Account |  30000 |
|    107 | Alex | Watt      | Lead       | Cash    |  28000 |
|    109 | Rick | Watt      | Probation  | Loan    |  30000 |
+--------+------+-----------+------------+---------+--------+
5 rows in set (0.00 sec)

---------------------------------------------------------------------------------------------------------------------------------------------------
USE OF IN AND NOT IN
--------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees
    -> where dept IN('Loan','Cash','Account');
+--------+------+-----------+-----------+---------+--------+
| emp_id | name | last_name | desig     | dept    | Salary |
+--------+------+-----------+-----------+---------+--------+
|    101 | Raju | Sharma    | Manager   | Loan    |  37000 |
|    102 | Sham | Mohan     | Cashier   | Cash    |  25000 |
|    103 | Paul | Thomas    | Associate | Loan    |  32000 |
|    106 | Rick | Watt      | Manager   | Account |  30000 |
|    107 | Alex | Watt      | Lead      | Cash    |  28000 |
|    108 | John | Paul      | Manager   | Account |  31000 |
|    109 | Rick | Watt      | Probation | Loan    |  30000 |
+--------+------+-----------+-----------+---------+--------+
7 rows in set (0.00 sec)

mysql> select * from emplyees
    -> where dept NOT IN('Loan','Cash','Account');
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
+--------+--------+-----------+------------+----------+--------+
2 rows in set (0.00 sec)
-------------------------------------------------------------------------------------------------------------------------------------------------
BETWEEN - USE
-------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE Salary >= 30000 AND Salary <=32000;
+--------+------+-----------+-----------+---------+--------+
| emp_id | name | last_name | desig     | dept    | Salary |
+--------+------+-----------+-----------+---------+--------+
|    103 | Paul | Thomas    | Associate | Loan    |  32000 |
|    106 | Rick | Watt      | Manager   | Account |  30000 |
|    108 | John | Paul      | Manager   | Account |  31000 |
|    109 | Rick | Watt      | Probation | Loan    |  30000 |
+--------+------+-----------+-----------+---------+--------+
4 rows in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE Salary BETWEEN 30000 AND 32000;
+--------+------+-----------+-----------+---------+--------+
| emp_id | name | last_name | desig     | dept    | Salary |
+--------+------+-----------+-----------+---------+--------+
|    103 | Paul | Thomas    | Associate | Loan    |  32000 |
|    106 | Rick | Watt      | Manager   | Account |  30000 |
|    108 | John | Paul      | Manager   | Account |  31000 |
|    109 | Rick | Watt      | Probation | Loan    |  30000 |
+--------+------+-----------+-----------+---------+--------+
4 rows in set (0.00 sec)
---------------------------------------------------------------------------------------------------------------------------------------------------
CASE - Categary
-----------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select name,salary,
    -> CASE
    -> WHEN Salary >= 30000 THEN 'Higher Salary'
    -> ELSE 'Low Salary'
    -> END
    -> AS 'Salary Category'
    -> From emplyees;
+--------+--------+-----------------+
| name   | salary | Salary Category |
+--------+--------+-----------------+
| Raju   |  37000 | Higher Salary   |
| Sham   |  25000 | Low Salary      |
| Paul   |  32000 | Higher Salary   |
| Alex   |  28000 | Low Salary      |
| Victor |  26000 | Low Salary      |
| Rick   |  30000 | Higher Salary   |
| Alex   |  28000 | Low Salary      |
| John   |  31000 | Higher Salary   |
| Rick   |  30000 | Higher Salary   |
+--------+--------+-----------------+
9 rows in set (0.00 sec)

mysql> select name,salary,
    -> case
    -> when salary >=32000 Then 'Higher Salary'
    -> when salary >=30000 AND salary < 32000 Then 'Mid Salary'
    -> ELSE 'Low Salary'
    -> End
    -> AS 'Salary Category'
    -> from emplyees;
+--------+--------+-----------------+
| name   | salary | Salary Category |
+--------+--------+-----------------+
| Raju   |  37000 | Higher Salary   |
| Sham   |  25000 | Low Salary      |
| Paul   |  32000 | Higher Salary   |
| Alex   |  28000 | Low Salary      |
| Victor |  26000 | Low Salary      |
| Rick   |  30000 | Mid Salary      |
| Alex   |  28000 | Low Salary      |
| John   |  31000 | Mid Salary      |
| Rick   |  30000 | Mid Salary      |
+--------+--------+-----------------+
9 rows in set (0.00 sec)
---------------------------------------------------------------------------------------------------------------------
USE OF NULL AND NOT LIKE
----------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from person;
+------------+----------+---------------------+
| jd         | jt       | jdt                 |
+------------+----------+---------------------+
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-04-17 | 20:08:45 | 2025-06-17 07:32:54 |
| 2025-06-18 | 07:37:11 | 2025-06-18 07:37:11 |
+------------+----------+---------------------+
3 rows in set (0.00 sec)

mysql> select * from person
    -> WHERE jt is NULL;
Empty set (0.00 sec)

mysql> select * from person
    -> Where jd is Null;
Empty set (0.00 sec)

----------------------------------------------------------------------------------------------------------------------
USE OF NULL & NOT NILL
-------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees
    -> where name like 'R%';
+--------+------+-----------+-----------+---------+--------+
| emp_id | name | last_name | desig     | dept    | Salary |
+--------+------+-----------+-----------+---------+--------+
|    101 | Raju | Sharma    | Manager   | Loan    |  37000 |
|    106 | Rick | Watt      | Manager   | Account |  30000 |
|    109 | Rick | Watt      | Probation | Loan    |  30000 |
+--------+------+-----------+-----------+---------+--------+
3 rows in set (0.00 sec)

mysql> select * from emplyees
    -> where name NOT LIKE 'R%';
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
+--------+--------+-----------+------------+----------+--------+
6 rows in set (0.00 sec)
---------------------------------------------------------------------------------------------------------------------------------
Exercise - 7
----------------------------------------------------------------------------------------------------------------------------
QYESTION
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
-> Find employees whose salary are between 30000 to 40000
-> Find employees whose first name start with 'R' or 'S'
-> Find employee whose salary=25000 and department should be 'Cash'
-> Find employees from following designation Manager, Lead and Associate
->
+--------+--------+-------------+
| name   | salary | Salary in $ |
+--------+--------+-------------+
| Raju   |  37000 |    440.4762 |
| Sham   |  25000 |    297.6190 |
| Paul   |  32000 |    380.9524 |
| Alex   |  28000 |    333.3333 |
| Victor |  26000 |    309.5238 |
| Rick   |  30000 |    357.1429 |
| Alex   |  28000 |    333.3333 |
| John   |  31000 |    369.0476 |
| Rick   |  30000 |    357.1429 |
+--------+--------+-------------+

---------------------------------------------------------------------------------------------------------------------------------------------
ANSWER
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select * from emplyees
    -> where salary BETWEEN 30000 AND 40000;
+--------+------+-----------+-----------+---------+--------+
| emp_id | name | last_name | desig     | dept    | Salary |
+--------+------+-----------+-----------+---------+--------+
|    101 | Raju | Sharma    | Manager   | Loan    |  37000 |
|    103 | Paul | Thomas    | Associate | Loan    |  32000 |
|    106 | Rick | Watt      | Manager   | Account |  30000 |
|    108 | John | Paul      | Manager   | Account |  31000 |
|    109 | Rick | Watt      | Probation | Loan    |  30000 |
+--------+------+-----------+-----------+---------+--------+
5 rows in set (0.00 sec)

mysql> select * from emplyees
    -> WHERE name LIKE "R%" OR name LIKE "S%";
+--------+------+-----------+-----------+---------+--------+
| emp_id | name | last_name | desig     | dept    | Salary |
+--------+------+-----------+-----------+---------+--------+
|    101 | Raju | Sharma    | Manager   | Loan    |  37000 |
|    102 | Sham | Mohan     | Cashier   | Cash    |  25000 |
|    106 | Rick | Watt      | Manager   | Account |  30000 |
|    109 | Rick | Watt      | Probation | Loan    |  30000 |
+--------+------+-----------+-----------+---------+--------+
4 rows in set (0.00 sec)

mysql> select * from emplyees
    -> where salary = 25000 AND dept = 'Cash';
+--------+------+-----------+---------+------+--------+
| emp_id | name | last_name | desig   | dept | Salary |
+--------+------+-----------+---------+------+--------+
|    102 | Sham | Mohan     | Cashier | Cash |  25000 |
+--------+------+-----------+---------+------+--------+
1 row in set (0.00 sec)
mysql> select * from emplyees
    -> WHERE desig in("Manager","Lead","Associate");
+--------+--------+-----------+-----------+----------+--------+
| emp_id | name   | last_name | desig     | dept     | Salary |
+--------+--------+-----------+-----------+----------+--------+
|    101 | Raju   | Sharma    | Manager   | Loan     |  37000 |
|    103 | Paul   | Thomas    | Associate | Loan     |  32000 |
|    105 | Victor | Das       | Associate | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager   | Account  |  30000 |
|    107 | Alex   | Watt      | Lead      | Cash     |  28000 |
|    108 | John   | Paul      | Manager   | Account  |  31000 |
+--------+--------+-----------+-----------+----------+--------+
6 rows in set (0.00 sec)

mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> select name,salary,
    -> CASE
    -> WHEN Salary!=0 Then salary/84
    -> END
    -> AS 'Salary in $'
    -> from emplyees;
+--------+--------+-------------+
| name   | salary | Salary in $ |
+--------+--------+-------------+
| Raju   |  37000 |    440.4762 |
| Sham   |  25000 |    297.6190 |
| Paul   |  32000 |    380.9524 |
| Alex   |  28000 |    333.3333 |
| Victor |  26000 |    309.5238 |
| Rick   |  30000 |    357.1429 |
| Alex   |  28000 |    333.3333 |
| John   |  31000 |    369.0476 |
| Rick   |  30000 |    357.1429 |
+--------+--------+-------------+
9 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
UNIQUE CONTRAIN
------------------------------------------------------------------------------------------------------------------------------------------------------------------------
mysql> Create table contact(
    -> mob VARCHAR(15) UNIQUE
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> desc contact;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(15) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.00 sec)

mysql> insert into contact values(123456);
Query OK, 1 row affected (0.00 sec)

mysql> select * from contact;
+--------+
| mob    |
+--------+
| 123456 |
+--------+
1 row in set (0.00 sec)

mysql> insert into contact values(1234567890);
Query OK, 1 row affected (0.01 sec)

mysql> insert into contact values(1234567890);
ERROR 1062 (23000): Duplicate entry '1234567890' for key 'contact.mob'
---------------------------------------------------------------------------------------------------------------------
CHECK CONSTRAINS - LESS THAN 10 DIGITS
---------------------------------------------------------------------------------------------------------------------
mysql> create table contact1(
    -> mob VARCHAR(15) UNIQUE CHECK(LENGTH(mob)>=10)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> desc contact1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(15) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.00 sec)

mysql>
mysql> insert into contact1 values(123456);
ERROR 3819 (HY000): Check constraint 'contact1_chk_1' is violated.
mysql> insert into contact1 values(1234567890);
Query OK, 1 row affected (0.00 sec)

mysql> insert into contact1 values(1234567891);
Query OK, 1 row affected (0.00 sec)

mysql> select * from contact1;
+------------+
| mob        |
+------------+
| 1234567890 |
| 1234567891 |
+------------+
2 rows in set (0.00 sec)

mysql> create table contact2(
    -> mob VARCHAR(15) UNIQUE,
    -> Constraint Mobno_is_less_Than_10Digits check(LENGTH(mob)>=10)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> desc contact2;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(15) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.00 sec)

mysql> insert into contact2 values(1234567890);
Query OK, 1 row affected (0.00 sec)

mysql> insert into contact2 values(123456789);
ERROR 3819 (HY000): Check constraint 'Mobno_is_less_Than_10Digits' is violated.
-----------------------------------------------------------------------------------------------------------
ALTERING TABLE
---------------------------------------------------------------------------------------------------------

mysql> ALTER TABLE Contact
    -> Add column name VARCHAR(50);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc contact;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(15) | YES  | UNI | NULL    |       |
| name  | varchar(50) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> select * from contact;
+------------+------+
| mob        | name |
+------------+------+
| 123456     | NULL |
| 1234567890 | NULL |
| 1234567891 | NULL |
+------------+------+
3 rows in set (0.00 sec)
------------------------------------------------------------------------------------------------------------------
DROP TABLE COLUMN ALTER
----------------------------------------------------------------------------------------------------------------
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(15) | YES  | UNI | NULL    |       |
| name  | varchar(50) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+

mysql> ALTER TABLE Contact
    -> Drop column name;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc contact;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(15) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.00 sec)

----------------------------------------------------------------------------------------------------------------
RENAMING A COLUMN AND TABLE NAME
----------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+--------+--------+-----------+------------+----------+--------+
| emp_id | name   | last_name | desig      | dept     | Salary |
+--------+--------+-----------+------------+----------+--------+
|    101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
|    102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
|    103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
|    104 | Alex   | Fernandes | Accountant | IT       |  28000 |
|    105 | Victor | Das       | Associate  | Deposite |  26000 |
|    106 | Rick   | Watt      | Manager    | Account  |  30000 |
|    107 | Alex   | Watt      | Lead       | Cash     |  28000 |
|    108 | John   | Paul      | Manager    | Account  |  31000 |
|    109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+--------+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> desc emplyees;
+-----------+-------------+------+-----+-----------+----------------+
| Field     | Type        | Null | Key | Default   | Extra          |
+-----------+-------------+------+-----+-----------+----------------+
| emp_id    | int         | NO   | PRI | NULL      | auto_increment |
| name      | varchar(50) | NO   |     | NULL      |                |
| last_name | varchar(50) | YES  |     | NULL      |                |
| desig     | varchar(50) | NO   |     | Probation |                |
| dept      | varchar(50) | NO   |     | NULL      |                |
| Salary    | int         | NO   |     | 25000     |                |
+-----------+-------------+------+-----+-----------+----------------+
6 rows in set (0.00 sec)
mysql> ALTER TABLE EMPLYEES
    -> RENAME COLUMN emp_id to id;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc emplyees;
+-----------+-------------+------+-----+-----------+----------------+
| Field     | Type        | Null | Key | Default   | Extra          |
+-----------+-------------+------+-----+-----------+----------------+
| id        | int         | NO   | PRI | NULL      | auto_increment |
| name      | varchar(50) | NO   |     | NULL      |                |
| last_name | varchar(50) | YES  |     | NULL      |                |
| desig     | varchar(50) | NO   |     | Probation |                |
| dept      | varchar(50) | NO   |     | NULL      |                |
| Salary    | int         | NO   |     | 25000     |                |
+-----------+-------------+------+-----+-----------+----------------+
6 rows in set (0.00 sec)

mysql> select * from emplyees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+-----+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------
HOW TO CHANGE A TABLE NAME
-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from emplyees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+-----+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)

mysql> ALTER Table emplyees
    -> RENAME TO Employees;
Query OK, 0 rows affected (0.02 sec)

mysql> select * from emplyees;
ERROR 1146 (42S02): Table 'bank_db.emplyees' doesn't exist
mysql> select * from employees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
+-----+--------+-----------+------------+----------+--------+
9 rows in set (0.00 sec)
mysql> desc employees;
+-----------+-------------+------+-----+-----------+----------------+
| Field     | Type        | Null | Key | Default   | Extra          |
+-----------+-------------+------+-----+-----------+----------------+
| id        | int         | NO   | PRI | NULL      | auto_increment |
| name      | varchar(50) | NO   |     | NULL      |                |
| last_name | varchar(50) | YES  |     | NULL      |                |
| desig     | varchar(50) | NO   |     | Probation |                |
| dept      | varchar(50) | NO   |     | NULL      |                |
| Salary    | int         | NO   |     | 25000     |                |
+-----------+-------------+------+-----+-----------+----------------+
6 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------
HOW TO ADD DEFAULT VALUE TO A COLUMN
-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> desc contact;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(15) | YES  | UNI | NULL    |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.00 sec)
mysql> ALTER TABLE contact
    -> MODIFY mob VARCHAR(20) DEFAULT 'UNKNOWN';
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc contact;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(20) | YES  | UNI | UNKNOWN |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.00 sec)
mysql> INSERT INTO contact (mob) VALUES ('Hello');
Query OK, 1 row affected (0.00 sec)

mysql> desc contact;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| mob   | varchar(20) | YES  | UNI | UNKNOWN |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.00 sec)

mysql> select * from contact;
+------------+
| mob        |
+------------+
| 123456     |
| 1234567890 |
| 1234567891 |
| Hello      |
+------------+
4 rows in set (0.00 sec)

mysql> INSERT INTO contact (mob) VALUES ('Hello');
ERROR 1062 (23000): Duplicate entry 'Hello' for key 'contact.mob'
-----------------------------------------------------------------------------------------------------------------------------------------------------
MANY TO MANYY
-----------------------------------------------------------------------------------------------------------------------------------------------------
CREATE DATABASE INSTITUTE;
Query OK, 1 row affected (0.02 sec)

mysql> use institute;
Database changed
mysql> CREATE TABLE students(
    -> id INT AUTO_INCREMENT PRIMARY KEY,
    -> student_name VARCHAR(250)
    -> );
Query OK, 0 rows affected (0.06 sec)

mysql> CREATE TABLE courses(
    -> id INT AUTO_INCREMENT PRIMARY KEY,
    -> student_name VARCHAR(250),
    -> FEES INT
    -> );
Query OK, 0 rows affected (0.06 sec)

mysql> show tables;
+---------------------+
| Tables_in_institute |
+---------------------+
| courses             |
| students            |
+---------------------+
2 rows in set (0.01 sec)

mysql> CREATE TABLE students_courses(
    -> students_id INT,
    -> courses_id INT,
    -> FOREIGN KEY (students_id) REFERENCES students(id),
    -> FOREIGN KEY (courses_id) REFERENCES courses(id)
    -> );
Query OK, 0 rows affected (0.08 sec)

mysql> show TABLES;
+---------------------+
| Tables_in_institute |
+---------------------+
| courses             |
| students            |
| students_courses    |
+---------------------+
3 rows in set (0.00 sec)

mysql> INSERT INTO students(student_name)
    ->  VALUES ('Raju'),('Sham'),('Paul'),('Alex');
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> INSERT INTO courses(id,student_name,fees)
    -> VALUES (101,'PD',3000);
Query OK, 1 row affected (0.02 sec)

mysql> INSERT INTO courses(student_name,fees)
    -> VALUES('java',5000),('SQL',40000),('Python',6000),('Linux',10000);
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> select * from students;
+----+--------------+
| id | student_name |
+----+--------------+
|  1 | Raju         |
|  2 | Sham         |
|  3 | Paul         |
|  4 | Alex         |
+----+--------------+
4 rows in set (0.00 sec)

mysql> select * from courses;
+-----+--------------+-------+
| id  | student_name | FEES  |
+-----+--------------+-------+
| 101 | PD           |  3000 |
| 102 | java         |  5000 |
| 103 | SQL          | 40000 |
| 104 | Python       |  6000 |
| 105 | Linux        | 10000 |
+-----+--------------+-------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE courses
    -> RENAME column student_name to course_name;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from courses;
+-----+-------------+-------+
| id  | course_name | FEES  |
+-----+-------------+-------+
| 101 | PD          |  3000 |
| 102 | java        |  5000 |
| 103 | SQL         | 40000 |
| 104 | Python      |  6000 |
| 105 | Linux       | 10000 |
+-----+-------------+-------+
5 rows in set (0.00 sec)

mysql> INSERT INTO students_courses(students_id, courses_id)
    -> VALUES (1, 101),(1, 102),(2, 105),(1, 105),(3, 103),(2, 102),(4, 104);
Query OK, 7 rows affected (0.03 sec)
Records: 7  Duplicates: 0  Warnings: 0

mysql> select * from students_courses;
+-------------+------------+
| students_id | courses_id |
+-------------+------------+
|           1 |        101 |
|           1 |        102 |
|           2 |        105 |
|           1 |        105 |
|           3 |        103 |
|           2 |        102 |
|           4 |        104 |
+-------------+------------+
7 rows in set (0.00 sec)

mysql> select * from students;
+----+--------------+
| id | student_name |
+----+--------------+
|  1 | Raju         |
|  2 | Sham         |
|  3 | Paul         |
|  4 | Alex         |
+----+--------------+
4 rows in set (0.00 sec)

mysql> SELECT student_name, course_name
    -> FROM students
    -> JOIN students_courses ON students.id = students_courses.students_id
    -> JOIN courses ON courses.id = students_courses.courses_id;
+--------------+-------------+
| student_name | course_name |
+--------------+-------------+
| Raju         | PD          |
| Raju         | java        |
| Raju         | Linux       |
| Sham         | Linux       |
| Sham         | java        |
| Paul         | SQL         |
| Alex         | Python      |
+--------------+-------------+
7 rows in set (0.00 sec)

-----------------------------------------------------------------------------------------------------------------------------------------------------
EXCERSISE - 09 SAME ABOVE tables
-----------------------------------------------------------------------------------------------
mysql> SELECT student_name, COUNT(course_name)
    -> FROM students
    -> JOIN students_courses ON students.id = students_courses.students_id
    -> JOIN courses ON courses.id = students_courses.courses_id
    -> GROUP BY student_name;
+--------------+--------------------+
| student_name | COUNT(course_name) |
+--------------+--------------------+
| Raju         |                  3 |
| Sham         |                  2 |
| Paul         |                  1 |
| Alex         |                  1 |
+--------------+--------------------+
4 rows in set (0.00 sec)

mysql> SELECT course_name, COUNT(student_name)
    -> FROM courses
    -> JOIN students_courses ON courses.id = students_courses.courses_id
    -> JOIN students ON students.id = students_courses.students_id
    -> GROUP BY course_name;
+-------------+---------------------+
| course_name | COUNT(student_name) |
+-------------+---------------------+
| PD          |                   1 |
| java        |                   2 |
| Linux       |                   2 |
| SQL         |                   1 |
| Python      |                   1 |
+-------------+---------------------+
5 rows in set (0.00 sec)

mysql> SELECT student_name, SUM(fees)
    -> FROM students
    -> JOIN students_courses ON students.id = students_courses.students_id
    -> JOIN courses ON courses.id = students_courses.courses_id
    -> GROUP BY student_name;
+--------------+-----------+
| student_name | SUM(fees) |
+--------------+-----------+
| Raju         |     18000 |
| Sham         |     15000 |
| Paul         |     40000 |
| Alex         |      6000 |
+--------------+-----------+
4 rows in set (0.00 sec)

-----------------------------------------------------------------------------------------------------------------------------------------------------
VIRTUAL TABLES
-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> CREATE VIEW insta_info AS
    -> SELECT student_name, course_name, fees
    -> FROM students
    -> JOIN students_courses ON students_courses.students_id = students.id
    -> JOIN courses ON students_courses.courses_id = courses.id;
Query OK, 0 rows affected (0.04 sec)

mysql> SELECT * FROM insta_info;
+--------------+-------------+-------+
| student_name | course_name | fees  |
+--------------+-------------+-------+
| Raju         | PD          |  3000 |
| Raju         | java        |  5000 |
| Raju         | Linux       | 10000 |
| Sham         | Linux       | 10000 |
| Sham         | java        |  5000 |
| Paul         | SQL         | 40000 |
| Alex         | Python      |  6000 |
+--------------+-------------+-------+
7 rows in set (0.00 sec)

mysql> SELECT student_name FROM insta_info;
+--------------+
| student_name |
+--------------+
| Raju         |
| Raju         |
| Raju         |
| Sham         |
| Sham         |
| Paul         |
| Alex         |
+--------------+
7 rows in set (0.00 sec)

mysql> SELECT * FROM insta_info WHERE student_name = 'Raju';
+--------------+-------------+-------+
| student_name | course_name | fees  |
+--------------+-------------+-------+
| Raju         | PD          |  3000 |
| Raju         | java        |  5000 |
| Raju         | Linux       | 10000 |
+--------------+-------------+-------+
3 rows in set (0.00 sec)

mysql> show tables;
+---------------------+
| Tables_in_institute |
+---------------------+
| courses             |
| insta_info          |
| students            |
| students_courses    |
+---------------------+
4 rows in set (0.00 sec)

mysql> drop view insta_info;
Query OK, 0 rows affected (0.02 sec)

mysql> show tables;
+---------------------+
| Tables_in_institute |
+---------------------+
| courses             |
| students            |
| students_courses    |
+---------------------+
3 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------
HAVING AND ROLLUP CLAUSE
-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> CREATE VIEW insta_info AS
    -> SELECT student_name, course_name, fees
    -> FROM students
    -> JOIN students_courses ON students_courses.students_id = students.id
    -> JOIN courses ON students_courses.courses_id = courses.id;
Query OK, 0 rows affected (0.04 sec)

mysql> SELECT * FROM insta_info;
+--------------+-------------+-------+
| student_name | course_name | fees  |
+--------------+-------------+-------+
| Raju         | PD          |  3000 |
| Raju         | java        |  5000 |
| Raju         | Linux       | 10000 |
| Sham         | Linux       | 10000 |
| Sham         | java        |  5000 |
| Paul         | SQL         | 40000 |
| Alex         | Python      |  6000 |
+--------------+-------------+-------+
7 rows in set (0.01 sec)

mysql> select student_name from insta_info GROUP BY student_name;
+--------------+
| student_name |
+--------------+
| Raju         |
| Sham         |
| Paul         |
| Alex         |
+--------------+
4 rows in set (0.00 sec)

mysql> select student_name, SUM(fees) from insta_info GROUP BY student_name;

+--------------+-----------+
| student_name | SUM(fees) |
+--------------+-----------+
| Raju         |     18000 |
| Sham         |     15000 |
| Paul         |     40000 |
| Alex         |      6000 |
+--------------+-----------+
4 rows in set (0.00 sec)

mysql> select student_name, SUM(fees) from insta_info GROUP BY student_name HAVING sum(fees)>10000;
+--------------+-----------+
| student_name | SUM(fees) |
+--------------+-----------+
| Raju         |     18000 |
| Sham         |     15000 |
| Paul         |     40000 |
+--------------+-----------+
3 rows in set (0.01 sec)

mysql> select student_name, SUM(fees) from insta_info GROUP BY student_name with rollup;
+--------------+-----------+
| student_name | SUM(fees) |
+--------------+-----------+
| Alex         |      6000 |
| Paul         |     40000 |
| Raju         |     18000 |
| Sham         |     15000 |
| NULL         |     79000 |
+--------------+-----------+
5 rows in set (0.02 sec)

mysql> select IFNULL(student_name,"TOTAL"), SUM(fees) from insta_info GROUP
BY student_name with rollup;
+------------------------------+-----------+
| IFNULL(student_name,"TOTAL") | SUM(fees) |
+------------------------------+-----------+
| Alex                         |      6000 |
| Paul                         |     40000 |
| Raju                         |     18000 |
| Sham                         |     15000 |
| TOTAL                        |     79000 |
+------------------------------+-----------+
5 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------
STORED ROUTINE
-----------------------------------------------------------------------------------------------------------------------------------------------------
select * from employees order by salary;

DELIMITER $$
CREATE procedure emp_info()
BEGIN
	select * from employees order by salary;
END $$

DELIMITER ;emp_info
IN WORKBENCH -> bank_db -> stored procedure -> emp_info -> click on right side button
call bank_db.emp_info();

select * from employees WHERE name = 'raju';					
-----------------------------------------------------------------------------------------------------------------------------------------------------
ARGUMENT PASSING IN STORED PROCEDURE
-----------------------------------------------------------------------------------------------------------------------------------------------------
DELIMITER $$

CREATE PROCEDURE get_emid(IN p_name VARCHAR(100))
BEGIN
    SELECT id 
    FROM employees 
    WHERE name = p_name;
END $$

DELIMITER ;

call bank_db.get_emid('raju');

-----------------------------------------------------------------------------------------------------------------------------------------------------
RETURNING OUTPUT IN A VARIABLE STORED PROCEDURE
-----------------------------------------------------------------------------------------------------------------------------------------------------
DELIMITER $$
REFRESH IT -> get_sum_by_dept to settings type loan

CREATE PROCEDURE get_sum_by_dept(IN p_dept VARCHAR(100), OUT p_sum DECIMAL(10, 2))
BEGIN
    SELECT SUM(salary) INTO p_sum 
    FROM employees 
    WHERE dept = p_dept;
END $$

DELIMITER ;


set @p_sum = 0;
call bank_db.get_sum_by_dept('loan', @p_sum);
select @p_sum;
-----------------------------------------------------------------------------------------------------------------------------------------------------
USER DEFINE FUNCTION
-----------------------------------------------------------------------------------------------------------------------------------------------------
DELIMITER $$

CREATE FUNCTION emp_name_max_salary() RETURNS VARCHAR(100)
DETERMINISTIC NO SQL READS SQL DATA 
BEGIN
	DECLARE v_max INT;
    DECLARE v_emp_name VARCHAR(100);
    SELECT MAX(salary) INTO v_max from employees;
    select name into v_emp_name FROM employees WHERE salary = v_max;
    
    return v_emp_name;
END $$

DELIMITER ;

go to bank_db to function -> given name function -> click on right side

select bank_db.emp_name_max_salary();

select * from employees;
-----------------------------------------------------------------------------------------------------------------------------------------------------

-----------------------------------------------------------------------------------------------------------------------------------------------------
select * from employees;

select sum(Salary) from employees;

select sum(Salary) over() as sum_salary from employees;

select 
id,
name,
sum(Salary)
 over() as sum_salary from employees;

 select 
id,
name,
salary,
sum(Salary) over(ORDER by id) as sum_salary from employees;

select 
id,
name,
salary,
max(Salary) over(ORDER by id) as sum_salary from employees;

select 
row_number() Over() as row_no, 
id,
dept,
salary,
salary from employees;

select 
row_number() Over(order by salary) as row_no, 
id,
dept,
salary,
salary from employees;

select 
row_number() Over(partition by dept) as row_no, 
id,
dept,
salary,
salary from employees;

select 
id,
dept,
salary,
RANK() OVER() as rank_sal from employees;

select 
id,
dept,
salary,
RANK() OVER(order by salary) as rank_sal from employees;

select 
id,
dept,
salary,
RANK() OVER(order by salary DESC) as rank_sal from employees;

select 
id,
dept,
salary,
DENSE_RANK() OVER(order by salary DESC) as rank_sal from employees;

select 
id,
dept,
salary,
LAG(salary) OVER() as diff_sal from employees;

select 
id,
dept,
salary,
LEAD(salary) OVER() as diff_sal from employees;

select 
id,
dept,
salary,
salary -LAG(salary) OVER(order by salary desc) as diff_sal from employees;

select 
id,
dept,
salary,
salary -LEAD(salary) OVER(order by salary desc) as diff_sal from employees;
-----------------------------------------------------------------------------------------------------------------------------------------------------
https://dev.mysql.com/doc/index-other.html
mysql -u root -p < employees.sql

-----------------------------------------------------------------------------------------------------------------------------------------------------
TRIGGERS
-----------------------------------------------------------------------------------------------------------------------------------------------------
use bank_db;

select * from employees;

insert into employees(name, last_name,desig,dept,salary)
VALUES('test','test','test','IT',-25000);

select * from employees;

DELIMITER //

CREATE TRIGGER trigger_before_insert
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 0 THEN
        SET NEW.salary = 0;
    END IF;
END//

DELIMITER ;

insert into employees(name, last_name,desig,dept,salary)
VALUES('test','test','test','IT',-25000);

select * from employees;

show triggers;

drop trigger trigger_before_insert;

show triggers;

-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> use bank_db;
Database changed
mysql> select * from employees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
| 110 | test   | test      | test       | IT       | -25000 |
| 111 | test   | test      | test       | IT       |      0 |
+-----+--------+-----------+------------+----------+--------+
11 rows in set (0.00 sec)

mysql> insert into employees(name, last_name,desig,dept,salary)
    -> VALUES('test','test','test','IT',-25000);
Query OK, 1 row affected (0.00 sec)

mysql> select * from employees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
| 110 | test   | test      | test       | IT       | -25000 |
| 111 | test   | test      | test       | IT       |      0 |
| 112 | test   | test      | test       | IT       | -25000 |
+-----+--------+-----------+------------+----------+--------+
12 rows in set (0.00 sec)

mysql> DELIMITER //
mysql>
mysql> CREATE TRIGGER trigger_before_insert
    -> BEFORE INSERT ON employees
    -> FOR EACH ROW
    -> BEGIN
    ->     IF NEW.salary < 0 THEN
    ->         SET NEW.salary = 0;
    ->     END IF;
    -> END//
Query OK, 0 rows affected (0.01 sec)

mysql>
mysql> DELIMITER ;
mysql> insert into employees(name, last_name,desig,dept,salary)
    -> VALUES('test','test','test','IT',-25000);
Query OK, 1 row affected (0.01 sec)

mysql> select * from employees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
| 110 | test   | test      | test       | IT       | -25000 |
| 111 | test   | test      | test       | IT       |      0 |
| 112 | test   | test      | test       | IT       | -25000 |
| 113 | test   | test      | test       | IT       |      0 |
+-----+--------+-----------+------------+----------+--------+
13 rows in set (0.00 sec)

mysql> show triggers;
+-----------------------+--------+-----------+------------------------------------------------------------------------------+--------+------------------------+-----------------------------------------------------------------------------------------------------------------------+----------------+----------------------+----------------------+--------------------+
| Trigger               | Event  | Table     | Statement
                                                | Timing | Created
      | sql_mode
                                                  | Definer        | character_set_client | collation_connection | Database Collation |
+-----------------------+--------+-----------+------------------------------------------------------------------------------+--------+------------------------+-----------------------------------------------------------------------------------------------------------------------+----------------+----------------------+----------------------+--------------------+
| trigger_before_insert | INSERT | employees | BEGIN
    IF NEW.salary < 0 THEN
        SET NEW.salary = 0;
    END IF;
END | BEFORE | 2025-06-19 19:40:44.47 | ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION | root@localhost | cp850                | cp850_general_ci     | utf8mb4_0900_ai_ci |
+-----------------------+--------+-----------+------------------------------------------------------------------------------+--------+------------------------+-----------------------------------------------------------------------------------------------------------------------+----------------+----------------------+----------------------+--------------------+
1 row in set (0.00 sec)

mysql>
mysql> drop trigger trigger_before_insert;
Query OK, 0 rows affected (0.01 sec)

mysql> show triggers;
Empty set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------
CTE - COMMON TABLE EXPRESSION
-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> select * from employees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
| 110 | test   | test      | test       | IT       | -25000 |
| 111 | test   | test      | test       | IT       |      0 |
| 112 | test   | test      | test       | IT       | -25000 |
| 113 | test   | test      | test       | IT       |      0 |
+-----+--------+-----------+------------+----------+--------+
13 rows in set (0.00 sec)

mysql> select dept,AVG(salary) from employees GROUP by dept;
+----------+-------------+
| dept     | AVG(salary) |
+----------+-------------+
| Loan     |  33000.0000 |
| Cash     |  26500.0000 |
| IT       |  -4400.0000 |
| Deposite |  26000.0000 |
| Account  |  30500.0000 |
+----------+-------------+
5 rows in set (0.00 sec)

mysql> WITH avg_sal AS (
    ->     SELECT dept, AVG(salary) AS avg_salary
    ->     FROM employees
    ->     GROUP BY dept
    -> )
    -> SELECT
    -> e.id, e.name, e.salary, a.avg_salary
    -> from employees e
    -> JOIN
    -> avg_sal a on e.dept=a.dept
    -> where
    -> e.salary>a.avg_salary;
+-----+------+--------+------------+
| id  | name | salary | avg_salary |
+-----+------+--------+------------+
| 101 | Raju |  37000 | 33000.0000 |
| 104 | Alex |  28000 | -4400.0000 |
| 107 | Alex |  28000 | 26500.0000 |
| 108 | John |  31000 | 30500.0000 |
| 111 | test |      0 | -4400.0000 |
| 113 | test |      0 | -4400.0000 |
+-----+------+--------+------------+
6 rows in set (0.00 sec)

mysql> WITH max_sal AS (
    -> SELECT dept, MAX(salary) AS max_salary
    -> FROM employees
    ->  GROUP BY dept
    -> )
    ->  SELECT
    -> e.id, e.name, e.dept, e.salary
    -> from employees e
    -> JOIN
    -> max_sal m on e.dept=m.dept
    ->  where
    ->  e.salary=m.max_salary;
+-----+--------+----------+--------+
| id  | name   | dept     | salary |
+-----+--------+----------+--------+
| 101 | Raju   | Loan     |  37000 |
| 104 | Alex   | IT       |  28000 |
| 105 | Victor | Deposite |  26000 |
| 107 | Alex   | Cash     |  28000 |
| 108 | John   | Account  |  31000 |
+-----+--------+----------+--------+
5 rows in set (0.00 sec)
-----------------------------------------------------------------------------------------------------------------------------------------------------
INDEX
-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| bank_db            |
| employees          |
| information_schema |
| institute          |
| mysql              |
| performance_schema |
| psadb1             |
| school_db          |
| store_db           |
| sys                |
+--------------------+
10 rows in set (0.00 sec)

mysql> use bank_db;
Database changed
mysql> select * from employees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
| 110 | test   | test      | test       | IT       | -25000 |
| 111 | test   | test      | test       | IT       |      0 |
| 112 | test   | test      | test       | IT       | -25000 |
| 113 | test   | test      | test       | IT       |      0 |
+-----+--------+-----------+------------+----------+--------+
13 rows in set (0.00 sec)

mysql> select * from employees where name = "Alex";
+-----+------+-----------+------------+------+--------+
| id  | name | last_name | desig      | dept | Salary |
+-----+------+-----------+------------+------+--------+
| 104 | Alex | Fernandes | Accountant | IT   |  28000 |
| 107 | Alex | Watt      | Lead       | Cash |  28000 |
+-----+------+-----------+------------+------+--------+
2 rows in set (0.00 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| bank_db            |
| employees          |
| information_schema |
| institute          |
| mysql              |
| performance_schema |
| psadb1             |
| school_db          |
| store_db           |
| sys                |
+--------------------+
10 rows in set (0.00 sec)

mysql> use employees;
Database changed

mysql> select * from employees limit 5;
+--------+------------+------------+-----------+--------+------------+
| emp_no | birth_date | first_name | last_name | gender | hire_date  |
+--------+------------+------------+-----------+--------+------------+
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 |
|  10002 | 1964-06-02 | Bezalel    | Simmel    | F      | 1985-11-21 |
|  10003 | 1959-12-03 | Parto      | Bamford   | M      | 1986-08-28 |
|  10004 | 1954-05-01 | Chirstian  | Koblick   | M      | 1986-12-01 |
|  10005 | 1955-01-21 | Kyoichi    | Maliniak  | M      | 1989-09-12 |
+--------+------------+------------+-----------+--------+------------+
5 rows in set (0.00 sec)
select * from employees

| 491231 | 1956-06-11 | Mihalis        | Farrag           | M      | 1994-02-06 |
| 491232 | 1958-03-15 | Marla          | Hasenauer        | M      | 1987-08-07 |
| 491233 | 1962-01-16 | Ohad           | Doering          | F      | 1985-06-22 |
| 491234 | 1959-02-26 | Mohit          | Sankaranarayanan | F      | 1987-06-27 |
| 491235 | 1961-12-11 | Gopalakrishnan | Makinen          | M      | 1992-03-25 |
| 491236 | 1963-07-26 | Malu           | Wiegley          | M      | 1989-11-27 |
| 491237 | 1954-06-21 | Avishai        | Bednarek         | M      | 1986-11-18 |
| 491238 | 1952-10-07 | Luise          | Soicher          | M      | 1985-11-20 |
| 491239 | 1958-01-25 | Danai          | Nanard           | M      | 1985-07-22 |
| 491240 | 1958-08-04 | Sasan          | Kemmerer         | F      | 1986-01-03 |
| 491241 | 1956-09-24 | Christoper     | Kropatsch        | F      | 1989-12-05 |
| 491242 | 1959-03-14 | Brewster       | Kleiser          | F      | 1997-07-27 |
| 491243 | 1962-08-26 | Ipke           | Welham           | M      | 1985-10-02 |
| 491244 | 1957-04-21 | Collette       | Berstel          | F      | 1985-04-08 |
| 491245 | 1961-11-24 | Mart           | Cappelletti      | M      | 1988-12-25 |
| 491246 | 1960-08-15 | Bowen          | Yurov            | F      | 1992-12-30 |
| 491247 | 1953-07-01 | Arch           | Macedo           | M      | 1989-01-05 |
| 491248 | 1953-06-23 | Rimli          | Perez            | M      | 1990-04-27 |
| 491249 | 1961-04-28 | Abdelghani     | Velardi          | F      | 1991-02-04 |
MORE

mysql> select * from employees where first_name = "gino";
+--------+------------+------------+---------------+--------+------------+
| emp_no | birth_date | first_name | last_name     | gender | hire_date  |
+--------+------------+------------+---------------+--------+------------+
|  10063 | 1952-08-06 | Gino       | Leonhardt     | F      | 1989-04-08 |
|  10860 | 1961-11-05 | Gino       | Werthner      | M      | 1992-03-11 |
|  11291 | 1953-11-01 | Gino       | Glowinski     | M      | 1985-10-20 |
|  11368 | 1959-07-31 | Gino       | Bail          | M      | 1992-01-06 |
|  12333 | 1964-05-01 | Gino       | Peck          | M      | 1990-09-20 |
|  12704 | 1962-09-08 | Gino       | Tetzlaff      | F      | 1994-07-16 |
|  13320 | 1954-08-04 | Gino       | Bahr          | F      | 1989-09-29 |
|  14177 | 1964-08-01 | Gino       | Stille        | F      | 1996-02-12 |
|  14256 | 1952-09-05 | Gino       | Ferriere      | F      | 1993-12-14 |
|  16981 | 1956-05-10 | Gino       | Fontan        | M      | 1998-10-20 |
|  18296 | 1957-08-21 | Gino       | Cesareni      | M      | 1994-09-04 |
-----------------------------------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------------------------------
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| bank_db            |
| employees          |
| information_schema |
| institute          |
| mysql              |
| performance_schema |
| psadb1             |
| school_db          |
| store_db           |
| sys                |
+--------------------+
10 rows in set (0.00 sec)

mysql> use bank_db;
Database changed
mysql> select * from employees;
+-----+--------+-----------+------------+----------+--------+
| id  | name   | last_name | desig      | dept     | Salary |
+-----+--------+-----------+------------+----------+--------+
| 101 | Raju   | Sharma    | Manager    | Loan     |  37000 |
| 102 | Sham   | Mohan     | Cashier    | Cash     |  25000 |
| 103 | Paul   | Thomas    | Associate  | Loan     |  32000 |
| 104 | Alex   | Fernandes | Accountant | IT       |  28000 |
| 105 | Victor | Das       | Associate  | Deposite |  26000 |
| 106 | Rick   | Watt      | Manager    | Account  |  30000 |
| 107 | Alex   | Watt      | Lead       | Cash     |  28000 |
| 108 | John   | Paul      | Manager    | Account  |  31000 |
| 109 | Rick   | Watt      | Probation  | Loan     |  30000 |
| 110 | test   | test      | test       | IT       | -25000 |
| 111 | test   | test      | test       | IT       |      0 |
| 112 | test   | test      | test       | IT       | -25000 |
| 113 | test   | test      | test       | IT       |      0 |
+-----+--------+-----------+------------+----------+--------+
13 rows in set (0.00 sec)

mysql> select * from employees where name = "Alex";
+-----+------+-----------+------------+------+--------+
| id  | name | last_name | desig      | dept | Salary |
+-----+------+-----------+------------+------+--------+
| 104 | Alex | Fernandes | Accountant | IT   |  28000 |
| 107 | Alex | Watt      | Lead       | Cash |  28000 |
+-----+------+-----------+------------+------+--------+
2 rows in set (0.00 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| bank_db            |
| employees          |
| information_schema |
| institute          |
| mysql              |
| performance_schema |
| psadb1             |
| school_db          |
| store_db           |
| sys                |
+--------------------+
10 rows in set (0.00 sec)

mysql> use employees;
Database changed

mysql> select * from employees limit 5;
+--------+------------+------------+-----------+--------+------------+
| emp_no | birth_date | first_name | last_name | gender | hire_date  |
+--------+------------+------------+-----------+--------+------------+
|  10001 | 1953-09-02 | Georgi     | Facello   | M      | 1986-06-26 |
|  10002 | 1964-06-02 | Bezalel    | Simmel    | F      | 1985-11-21 |
|  10003 | 1959-12-03 | Parto      | Bamford   | M      | 1986-08-28 |
|  10004 | 1954-05-01 | Chirstian  | Koblick   | M      | 1986-12-01 |
|  10005 | 1955-01-21 | Kyoichi    | Maliniak  | M      | 1989-09-12 |
+--------+------------+------------+-----------+--------+------------+
5 rows in set (0.00 sec)
mysql> select COUNT(emp_no) from employees;
+---------------+
| COUNT(emp_no) |
+---------------+
|        300024 |
+---------------+
1 row in set (0.01 sec)

mysql> select * from employees where first_name = "gino";
+--------+------------+------------+---------------+--------+------------+
| emp_no | birth_date | first_name | last_name     | gender | hire_date  |
+--------+------------+------------+---------------+--------+------------+
|  10063 | 1952-08-06 | Gino       | Leonhardt     | F      | 1989-04-08 |
|  10860 | 1961-11-05 | Gino       | Werthner      | M      | 1992-03-11 |
|  11291 | 1953-11-01 | Gino       | Glowinski     | M      | 1985-10-20 |
|  11368 | 1959-07-31 | Gino       | Bail          | M      | 1992-01-06 |
|  12333 | 1964-05-01 | Gino       | Peck          | M      | 1990-09-20 |
|  12704 | 1962-09-08 | Gino       | Tetzlaff      | F      | 1994-07-16 |
|  13320 | 1954-08-04 | Gino       | Bahr          | F      | 1989-09-29 |
|  14177 | 1964-08-01 | Gino       | Stille        | F      | 1996-02-12 |
|  14256 | 1952-09-05 | Gino       | Ferriere      | F      | 1993-12-14 |
|  16981 | 1956-05-10 | Gino       | Fontan        | M      | 1998-10-20 |
|  18296 | 1957-08-21 | Gino       | Cesareni      | M      | 1994-09-04 |
|  18863 | 1957-08-30 | Gino       | Perez         | M      | 1992-05-17 |
|  20471 | 1958-05-21 | Gino       | Haumacher     | F      | 1989-11-18 |
|  23494 | 1962-06-12 | Gino       | Deyuan        | M      | 1994-01-31 |
more (0.20 sex)

mysql> create index i_name on employees(first_name);
Query OK, 0 rows affected (0.76 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from employees where first_name = "gino";
+--------+------------+------------+---------------+--------+------------+
| emp_no | birth_date | first_name | last_name     | gender | hire_date  |
+--------+------------+------------+---------------+--------+------------+
|  10063 | 1952-08-06 | Gino       | Leonhardt     | F      | 1989-04-08 |
|  10860 | 1961-11-05 | Gino       | Werthner      | M      | 1992-03-11 |
|  11291 | 1953-11-01 | Gino       | Glowinski     | M      | 1985-10-20 |
|  11368 | 1959-07-31 | Gino       | Bail          | M      | 1992-01-06 |
|  12333 | 1964-05-01 | Gino       | Peck          | M      | 1990-09-20 |
|  12704 | 1962-09-08 | Gino       | Tetzlaff      | F      | 1994-07-16 |
|  13320 | 1954-08-04 | Gino       | Bahr          | F      | 1989-09-29 |
|  14177 | 1964-08-01 | Gino       | Stille        | F      | 1996-02-12 |
|  14256 | 1952-09-05 | Gino       | Ferriere      | F      | 1993-12-14 |
|  16981 | 1956-05-10 | Gino       | Fontan        | M      | 1998-10-20 |
|  18296 | 1957-08-21 | Gino       | Cesareni      | M      | 1994-09-04 |
|  18863 | 1957-08-30 | Gino       | Perez         | M      | 1992-05-17 |
|  20471 | 1958-05-21 | Gino       | Haumacher     | F      | 1989-11-18 |
|  23494 | 1962-06-12 | Gino       | Deyuan        | M      | 1994-01-31 |
more (0.04 sec)

mysql> show indexes from employees;
+-----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table     | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| employees |          0 | PRIMARY  |            1 | emp_no      | A         |      299335 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| employees |          1 | i_name   |            1 | first_name  | A         |        1328 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
+-----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
2 rows in set (0.01 sec)

mysql> ALTER table employees
    -> drop index i_name;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show indexes from employees;
+-----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table     | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| employees |          0 | PRIMARY  |            1 | emp_no      | A         |      299335 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
+-----------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
1 row in set (0.00 sec)
---------------------------------------------------------------------------------------------------------------------------------------

            
