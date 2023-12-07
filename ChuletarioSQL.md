## SETUP ububtu 22.04
```
[linuxuser@linuxserver ~]$ sudo apt update
[linuxuser@linuxserver ~]$ sudo apt install mysql-server
[linuxuser@linuxserver ~]$ sudo mysql_secure_installation
// Configuramos el nivel de complejidad de contraseña
// Deshabilitamos acceso remoto del usuario root
// No permitimos el acceso de usuarios anónimos

[linuxuser@linuxserver ~]$ sudo mysql -u root
sql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
sql> CREATE USER 'nombre_usuario'@'%' IDENTIFIED BY 'tu_contraseña';
sql> GRANT ALL PRIVILEGES ON *.* TO 'nombre_usuario'@'%';
sql> FLUSH PRIVILEGES;
sql> exit

[linuxuser@linuxserver ~]$ sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 0.0.0.0
mysqlx-bind-address = 0.0.0.0

[linuxuser@linuxserver ~]$ sudo systemctl restart mysql


// Revisamos los logs en /var/log/mysql/error.log
[linuxuser@linuxserver ~]$ tail -f /var/log/mysql/error.log
```

## DATABASE
```
sql> CREATE DATABASE <database_name>;
sql> USE <database_name>;
sql> DROP DATABASE <database_name>;
```

## TABLE
### CREATE TABLE
```
sql> CREATE TABLE <table_name> (
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  age INT,
  PRIMARY KEY (id),
  FOREIGN KEY (age) REFERENCES OtherTable(age)
);
```
#### DATA TYPES
| Data Type | Descripción |
|:--------:|-------------|
| VARCHAR(size) | A VARIABLE length string (can contain letters, numbers, and special characters). The size parameter specifies the maximum string length in characters - can be from 0 to 65535. |
| BOOL | Zero is considered as false, nonzero values are considered as true. |
| INT(size) | A medium integer. Signed range is from -2147483648 to 2147483647. Unsigned range is from 0 to 4294967295. The size parameter specifies the maximum display width (which is 255). |
| FLOAT(p) | A floating point number. MySQL uses the p value to determine whether to use FLOAT or DOUBLE for the resulting data type. If p is from 0 to 24, the data type becomes FLOAT(). If p is from 25 to 53, the data type becomes DOUBLE(). |
| DECIMAL(size, d) | An exact fixed-point number. The total number of digits is specified in size. The number of digits after the decimal point is specified in the d parameter. The maximum number for size is 65. The maximum number for d is 30. The default value for size is 10. The default value for d is 0. |
| DATE | A date. Format: YYYY-MM-DD. The supported range is from '1000-01-01' to '9999-12-31'. |
| DATETIME(fsp) | A date and time combination. Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1000-01-01 00:00:00' to '9999-12-31 23:59:59'. Adding DEFAULT and ON UPDATE in the column definition to get automatic initialization and updating to the current date and time. |
| TIMESTAMP(fsp) | A timestamp. TIMESTAMP values are stored as the number of seconds since the Unix epoch ('1970-01-01 00:00:00' UTC). Format: YYYY-MM-DD hh:mm:ss. The supported range is from '1970-01-01 00:00:01' UTC to '2038-01-09 03:14:07' UTC. Automatic initialization and updating to the current date and time can be specified using DEFAULT CURRENT_TIMESTAMP and ON UPDATE CURRENT_TIMESTAMP in the column definition |
| TIME(fsp) | A time. Format: hh:mm:ss. The supported range is from '-838:59:59' to '838:59:59' | |

### DROP TABLE
```
sql> DROP TABLE <table_name>;
```

### ALTER TABLE
#### ADD
```
sql> ALTER TABLE <table_name> ADD <column_name> <datatype>;
```
#### DROP
```
sql> ALTER TABLE <table_name> DROP COLUMN <column_name>;
```
#### RENAME
```
sql> ALTER TABLE <table_name> RENAME COLUMN <old_name> to <new_name>;
```
#### MODIFY DATA TYPE
```
sql> ALTER TABLE <table_name> MODIFY COLUMN <column_name> <datatype>;
```
#### CHANGE PRIMARY KEY
```
sql> ALTER TABLE <table_name> DROP PRIMARY KEY, ADD <column_name> <datatype> PRIMARY KEY;
```
#### CHANGE COLUMN POSITION
```
sql> ALTER TABLE <table_name> MODIFY COLUMN <column_name> <datatype> AFTER <other_column_name>;
```
#### ADD FOREING KEY
```
sql> ALTER TABLE <table_name> ADD FOREIGN KEY (<existent_column1>) REFERENCES <other_table_name_existent>(<column1>);
```

## OPERACIONES CRUD
### CREATE / INSERT
```
sql> INSERT INTO <table_name> (<column1>, <column2>, <column3>, ...) VALUES (<value1>, <value2>, <value3>, ...);
```
### READ / SELECT
```
sql> SELECT * FROM <table_name>;
sql> SELECT <column1>, <column2>... FROM <table_name> WHERE <column1> = 'Lluís' ;
```
### UPDATE
```
sql> UPDATE <table_name> SET <column1> = 52 WHERE <column2> = 'Zaragoza';
```
### DELETE
```
sql> DELETE FROM <table_name> WHERE <column2> = 'Zaragoza';
```
### COMMIT TO SAVE TRANSACTIONS
```
sql> COMMIT;
```
