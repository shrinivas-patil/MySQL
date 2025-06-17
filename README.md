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

