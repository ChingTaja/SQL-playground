<!-- Data Types https://dev.mysql.com/doc/refman/8.4/en/data-types.html -->
1. numberic types
- INT (e.g. 18 , -1999 , 0)

2. string types
- varchar (e.g. 'coo=ffe', '-1333' )

3. date types

#### CHAR vs. VARCHAR
char 存取資料 -> 有固定長度
varchar 存取資料 -> 沒有固定長度


#### Number Type
spec: https://dev.mysql.com/doc/refman/8.4/en/integer-types.html

unsigned means no negative

#### Decimal （more exact, take more space）--> 更精確
- （up to total number of digits,up to digits after decimal）
```SQL
Decimal(5,2)
```
![alt text](<截圖 2025-09-18 晚上10.46.14.png>)

#### float & double (stoer more larger decimal using less space, but it comes at the **cost of precision** )
![alt text](image.png)
```SQL
-- persume x is float
-- persume y is double
INSERT INTO nums(x,y) VALUES (1.12345678, 1.908789789789)
-- x 1.123456 (7 digits)
-- y 1.12345678 (15 digits)

INSERT INTO nums(x,y) VALUES (1.12345678, 1.9087897897898789789678678)
-- x 1.123456 (7 digits)
-- y 1.12345678 (15 digits)
```