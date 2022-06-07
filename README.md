# BLOG-DB

MYSQL is a relational dbms, data stored in different tables which can increase speed and felexibility.
Use SQL language, open source.
Afterdownload mysql and sqlyog, start using in cmd
mysql -uroot -ppassword then enter to link to the sql.
mysql -uroot -ppassword --link to the mysql 
flush privileges --refresh authery

basic command line for sql:
all the request use ; to finish.
show databases; --show all the databases
use databasename; --change to databasename database, `use` command
show tables; --check all the tables
describe tablename; --show information of table tablename
create database databasename; --create databasename database
exit; --quit sql

sql use "--" for explaination, # is only accepted in sqlyog
/* explaination content*/ multiline of explaination
----------------------------------------------------------

DB core function is CRUD
DDL Data Definition Language
DML Data Manipulation Language ****important****
DQL Data Query Language
DCL Data Control Language

---------------------------------------------------
OPERATE DB
CREATE DATABASE IF NOT EXISTS DATABASENAME; --if databasename database does not exist, create it. [IF NOT EXISTS] is chooseable.
DROP DATABASE IF EXISTS DATABASENAME; --DELETE DATABASENAME DATABASE IS EXIST.  [IF EXISTS] is chooseable.

-------------------------------------------
data types

VALUE:
tinyint: 1 byte
small int: 2 byte
dediumint: 3 byte
int: 4 byte
bigint: 8 byte
float: 4 byte
double: 8 byte
decimal: use for financial calculate

STRING:
char: fixed string 0-255
varchar: commonly used string 0-65535
tinytext: 2^8-1
text: 2^16-1

DATA and TIME:
date: YYYY-MM-DD date
time: HH:mm:ss  time
daytime: YYYY-MM-DD HH:mm:ss  most used format
timastamp: return the ms from 1970.1.1 to now. commonly used

NULL:
no value, unkown.
use NULL for calculate, the result will be null.


DATABASE field properties
Unsigned: unsigned integer. cannot be declared to a negative number.
zerofill: use 0 to fill the position undefined.  --example: int(3), 5 --005.
auto increment: auto increase 1 based on last record. used to design unique primary key and customize primary key.
null and  not null: without value, null is null and not null is erro
default:not declare value, the initial value.

each table include 5 points: id(primary key), `version`, is_delete, gmt_ create, gmt_update

-------------------------------------------------------------------
common create a table:
CREATE TABLE IF NOT EXISTS `student` (
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT'studentID',
	`name` VARCHAR(30) NOT NULL DEFAULT 'unkown' COMMENT 'name',
	`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT 'password',
	`sex` VARCHAR(10) NOT NULL DEFAULT 'female' COMMENT 'sex',
	`birthday` DATETIME DEFAULT NULL COMMENT 'birthday',
	`address` VARCHAR(100) DEFAULT NULL COMMENT 'family address',
	`email` VARCHAR(50) DEFAULT NULL COMMENT 'email address',
	PRIMARY KEY(`id`)

) ENGINE INNODB DEFAULT CHARSET = utf8

CREATE TABLE IF NOT EXISTS `table name` (
	`field name`  type  Attributes  index  Notes,
  `field name`  type  Attributes  index  Notes,
  `field name`  type  Attributes  index  Notes

) ENGINE  CHARSET
----------------------------------------------------

INNODB MYISAM adifference:

                                                MYISAM                              INNODB
Transaction support                            no support                           support
data row locking                               no support                           support
foreign key constraints                        no support                           support
full text index                                support                              no support
tablespace size	                               smaill                               big, about 2 times than MYISAM

NORMAL USE:
MYISAM: fast speed, save space.
INNODB:more safety, transaction support, multiple table mtiple users operate.

IN PHYSICAL SPACE:
all database files saves under data directory


MYSQL engine in PHYSICAL:
INNODB: relate to one *.frm file, and upper dir ibdata1 file
MYISAM:
*.frm: table strusture definition
*.myd: data
*.myi:index

CHANGE table:
ALERT TABLE tablename RENAME As newtablename; --CHANGE THE NAME OF TABLE
ALERT TABLE TABLENAME ADD `new field name` int(11);  -- add a new field name to the table.
ALERT TABLE tablename MODIFY `field name` new type; --modify is used to change the type of name field. instance change int(11) to char(20)
ALERT TABLE tablename CHANGE `field name` CHANGE oldname newname newtype; --change is used to change new name.
ALERT TABLE tablename DROP `field name`; --delete the field name of one table.

DELETE table:
DROP TABLE IF EXISTS table name;  --delete tablename table if it exists

ALL CREATE and DELETE operation should add constrain to avoid of fail.


DML language:
insert:
INSERT INTO `TABLENAME` (`FIELD NAME1`, `FIELD NAME2`, `FIELD NAME3`) VALUES ('DETAILVALUE1', 'DETAILVALUE1', 'DETAILVALUE1'),  ('DETAILVALUE4', 'DETAILVALUE5', 'DETAILVALUE6')   --VALUE in the quote must be match to the field name. 

update:
UPDATE table name SET COLUMN_NAME = value WHERE constrain;
UPDATE `student` SET `name` = 'QILUNBU', `email` = 'qbuu0001@qq.com' WHERE `id` = 1;


WHERE:
<> and != means not equal. 

DELETE:
DELETE FROM table name WHERE constrains

TRUNCATE:
totally remove a table in one database, while the index and stucture not

DELETE different with TRUNCATE:
clear data keep the structure;
TRUNCATE:
refresh the self increment key and counter roll back to 0.
not influence transaction support

DELETE:
not influence the self increment value. The value will countinue from the last value.


WHen we use DELETE, when the dabatase is restarted, INNODB the self increment column will start from 0 because the data is stored in the memory.
MYISAM save data in the file, the self increment colomn will increase from last record.

DQL ****most important****
SELECT always used

SELECT `studentName` from student   --select specific name from table dtudent
SELECT `studentName` AS NAME, `studentID` AS ID from student --AS give the column information a new name to understand easier
SELECT CONCAT('displayname', `studentName`) as NEWNAME from Student; --concat combine the 'information' and `studentName` together and the name of the result is NEWNAME

SELECT DICTINCt `studentID` FROM student;  --DISTINCT is used for remove duplicate
SELECT `studentID`, `studentResult`+1 as NEWMARK from result -- can direct use +-*/ in the query language

FUZZY QUERY:  LIKE
WHERE studentName LIKE 'LIU%'    --select name only with LIU start
WHERE studentName LIKE 'LIU_'    --select name only with LIU start and only follow 1 word
WHERE studentName LIKE 'LIU__'   --select name only with LIU start and only follow 2 word
WHERE studentName LIKE '%JIA%'   --select name with JIA in the name

WHERE studentID IN (1001, 1002, 1003)   --IN means select value in 1001, 1002 and 1003.

JOIN SEARCH:
1. Think about the request, where does all these info come from which tables.
2. Make sure which part we wanna join and common part


SELECT s.studentNo, studentName, subjectNo, studentResult
FROM student AS s
INNER JOIN result AS r
ON s.studentNo = r.studentNo

operation        description                                                                      d
inner join       field name in each table will return if both exist, declare in which table
left join        Though the right table does not have the match, still return all the value from the left table
right join       Though the left table does not have all the value, still return all the value from the right table


SELECT s.studentNo, studentName, subjectNo, studentResult
FROM student AS s
LEFT JOIN result AS r
ON s.studentNo = r.studentNo
WHERE studentResult IS NULL


JOIN ON    JOIN(link tables) ON(constrains)--link query
WHERE --equal query

Three tables join search:
Make sure what information you want, base on the information you want, select tables. 

sassume that the information we want is .
**studentId belongs to the table Student and table result. SubjectNo belongs to table result and table subject**
what we want to do is find ways to join all these tables together.

SELECT s.studentId, studentName, seubjectNo, stuntResult    --just select these first, then we will make sure each detail during the join
FROM student AS s 
RIGHT JOIN result AS r
ON s.studentID = r.studentID    --at this stage, there  will be confuse about the studentID, so we need to make sure which studentNo.
                               --also at this stage, we get a new table, base on this table we go to join another table to create a new table
INNER JOIN `subject` AS sub    --we already have s for student table, at this stage, we will keep use sub as new name for subject. 
ON r.subjectNo = sub.subjectNo --like we did past, we need to find a new link point for the new table and the previous two joined table we choosed.


ORDER BY:
based on the constrain to order the results. DESC to order the result from high to low. ASC to order the result from high to low.
ORDER BY studentResult DESC  --order the result based on the result of score, from high to low.

SELECT s.studentId, studentName, seubjectNo, stuntResult 
FROM student AS s 
RIGHT JOIN result AS r
ON s.studentID = r.studentID   
INNER JOIN `subject` AS sub   
ON r.subjectNo = sub.subjectNo
OEDER BY studentResult DESC

SEPERATE PAGE:
LIMIT num1, num2  --num1: means the start position of the result (1st position start at 0)
                  --num2: means that how many results on this page.

SELECT s.studentId, studentName, seubjectNo, stuntResult 
FROM student AS s 
RIGHT JOIN result AS r
ON s.studentID = r.studentID   
INNER JOIN `subject` AS sub   
ON r.subjectNo = sub.subjectNo
WHERE subjectNo = 'XXXXX'
OEDER BY studentResult DESC
LIMIT 0, 5   --start position is the first one and the size of this page is 5.

MYSQL function:
MATH :
SELECT ABS(-8) --8
SELECT CEILING(9.4) --10
SELECT FLOOR(9.4) --9
SELECT RAND  --OUTPUT IS A RANDOM NUMBER BETWEEN 0-1
SELECT SIGN(-10)  --NEGATIVE RETURN -1
SELECT SIGN(10)   --POSITIVE RETURN 1
SELECT SIGN(0)    --0 RETURN 0

STRING function:
SELECT CHAR_LENGTH('hellio')  --RETURN THE LENGTH OF THE STRING 6
SELECT CONCAT('I', 'LOVE', 'U')   --CONCAT the content in the ''
SELECT INSERT('ILOVECODINGhelloworld', 1, 2, 'howru')  --USE THE LAST CONTENT REPLACE FRONT CONTENT, START FROM 1, END TO WHERE, THE CONTENT LISTED WILL BE REPLACED BY THE LAST CONTENT.
SELECRT LOWER(TryndamereBQL)  --change the content to lower case
SELECT UPPER(TryndamereBQL)    --change the content to upper case
SELECT INSTR('TryndamereBQL', 'BQL')   --show the index of substring 'BQL' appear in the string 'tryndamerebql'.
SELECT REPLACE('ILOVE CODING', 'CODING', 'PLAYING')    --use PLAYING replace CODING
SELECT SUBSTR('ILOVECODING', 4, 3)   --return the string hyou want, 4 means starting index and 3 means how long the string u want
SELECT REVERSE('ILOVECODING')     --reverse the content
SELECT CURRENT_DATE()   --get current date 
SELECT LOCALTIME()   --get lical time


Aggregate function
COUNT()            --count number
SUM()              --total number
AVG()              --average value
MAX()              --max num
MIN()              --min value

SELECT COUNT(studentName) FROM studenbt;  --COUNT(fieldname)  ignore all the NULL value
SELECT COUNT(*) FROM studenbt;            --COUNT(*) count all inculde null value
SELECT COUNT(1) FROM studenbt;            --COUNT(1) count all inculde null value

SELECT SUM(`studentResult`) AS `total` FROM result   --result total
SELECT AVG(`studentResult`) AS `average` FROM result   --result average
SELECT MAX(`studentResult`) AS `max` FROM result   --result max
SELECT MIN(`studentResult`) AS `min` FROM result   --result min

TRANSITION PROCESSING:
ATOMICITY:  transition successful together or fail together
CONSISTENCY: before operation and after operation, keep same total
ISOLATION: 
DURABILITY: transactin not commit, roll back.  transactin committed, save to file and not changed. traactin commited, cant be rolled back.


INDEX:
CREATE INDEX id_app_user_name ON app_user(`name`);  --CREATE INDEX index name  ON table(field name)


JDBC:
application cannot directly connect to the database, need a deive to link.

First JDBC project:
1. create a normal database


CREATE DATABASE jdbcStudy CHARSET SET utf8 COLLATE utf8_general_ci;
USE jdbcStudy;
CREATE TABLE users(
	`id` INT PRIMARY KEY,
	`name` VARCHAR(40),
	`password` VARCHAR(40),
	`email` VARCHAR(60),
	`birthday` DATE
);

INSERT INTO users(`id`, `name`, `password`, `email`, `birthday`)
VALUES(1, 'zhangsan', '123456', 'zs@sina.com', '1980-12-04'), (2, 'lisi', '123456', 'lisi@sina.com', '1981-12-04'), (3, 'wangwu', '123456', 'wangwu@sina.com', '1979-12-04');


2.import database drive:
import mysql-connector-java-5.1.47.jar into a lib dir which is created under the project, copy it to the dir and add it as a library, then this step finish.

3.steps conclusion:
package com.qilun.lesson01;

import java.sql.*;

//my first jdbc project
public class jdbcFirstDemo {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //1.load driver
        Class.forName("com.mysql.jdbc.Driver"); //fixed writing, load driver

        //2.use user info and url link to database
        String url = "jdbc:mysql://localhost:3306/jdbcStudy?useUnicode=true&characterEncoding=utf8&userSSL=true";
        String username = "root";
        String password = "hsp";

        //3.connect success, database obj
        Connection connection = DriverManager.getConnection(url, username, password);

        //4.get sql statement
        Statement statement = connection.createStatement();

        //5.see the result
        String sql = "SELECT * FROM users";
        ResultSet resultSet = statement.executeQuery(sql);
        while (resultSet.next()){
            System.out.println("id=" + resultSet.getObject("id"));
            System.out.println("name=" + resultSet.getObject("name"));
            System.out.println("password=" + resultSet.getObject("password"));
            System.out.println("email=" + resultSet.getObject("email"));
            System.out.println("birthday=" + resultSet.getObject("birthday"));
        }
        //6.release connection
        resultSet.close();
        statement.close();
        connection.close();





    }
}



Statement operate SQL object: prepareStatement
Statement is used to send sql request to the database.
statement.executeUpdate(): send crud request to the database
statement.executeQuery(): send query language the the database.
















































