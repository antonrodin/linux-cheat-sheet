MySQL
======

Some basic commands to connect, select dabatase or create user

Oficial 8.0 MySQL Documentation: https://dev.mysql.com/doc/relnotes/mysql/8.0/en/

Login into MySQL and database, examples

```shell
mysql -u root -p
mysql -u anton -p
mysql -h host -u user -p database_name
```

Show Databases

```MySQL
SHOW DATABASES;
SHOW SHEMAS;
```

Create new database, the **utf8mb4** now is the best practice, the old 

**utf8_general_ci** is not longer considered recomended

```mysql
CREATE DATABASE anton_database CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Select Database

```MySQL
USE anton_database;
```

Create user & Password for MySQL and drom user...

```mysql
CREATE USER 'anton'@'localhost' IDENTIFIED BY '1234';
DROP USER ‘anton’@‘localhost’;
```
Also you can delete the row __from mysql.users__... I guess its not the best options, but sometimes you should do it, then the permission is not right is one way to do this.

How to show users

```mysql
SELECT * FROM mysql.user;
SELECT host, user, password FROM mysql.user;
```

Grant permision on custom database for custom user or ALL Privileges, like root user.
Therefore is better practice I guess to grant "custom" priveleges for users...

```mysql
# Custom privileges only for anton_database
GRANT ALL ON anton_database.* TO 'anton'@'localhost';

# Global Privileges
GRANT ALL PRIVILEGES ON * . * TO 'antonrodin'@'localhost';

# Grant privileges for remote access from any IP, % is a Wild Card
GRANT ALL ON anton_database.* TO 'anton'@'%' IDENTIFIED BY 'Password';
GRANT ALL ON *.* TO 'anton'@'%' IDENTIFIED BY 'Password';

# Dont forget to Flush Privileges
FLUSH PRIVILEGES;
```
Show Grants

```mysql
SHOW GRANTS FOR 'anton'@'localhost';
```

Change user password
```mysql
SET PASSWORD FOR 'anton'@'localhost' = PASSWORD('auth_string');
SET PASSWORD FOR 'anton'@'localhost' = 'auth_string';
```

## Grant remote access, some file configuration

```shell
#Edit the custom files
vi /etc/mysql/my.cnf
vi /etc/my.cnf
```

Edit:
```Coment following lines
#bind-address           = 127.0.0.1
#skip-networking
```


Also rstar MySQL Service
```shell
service mysql restart
```

Rememeber to grant remote access for root or other users...
Good luck my dear friend...