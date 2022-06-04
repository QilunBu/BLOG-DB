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
DML Data Manipulation Language
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

















































