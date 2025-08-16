```SQL
SHOW DATABASES;
SHOW tables;
SHOW COLUMNS FROM cats;
DESC cats; --DESCRIBE

CREATE DATABASE soap_store; 

DROP DATABASE soap_store;
DROP TABLE cats;

USE soap_store;

SELECT database()

CREATE TABLE cats (
    name VARCHAR(50),
    age INT
);
```