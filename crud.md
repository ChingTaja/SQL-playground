```SQL
-- insert
INSERT INTO cats (name, age) 
VALUES ('Blue Steele', 5);

-- get
SELECT * FROM cats;

-- multiple insert
INSERT INTO cats (name, age) 
VALUES 
  ('Meatball', 5), 
  ('Turkey', 1), 
  ('Potato Face', 15);
```

NULL means the lack of value (no information)


#### add constraint (NOT  NULL)

NULL yes --> permit null
NULL no --> forbidden null

```SQL
CREATE TABLE cats2 (
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL
);
```
Some systems permit the use of single quotes (''), but it is safer to use double quotes ("").


#### add default value

Having a default value in SQL doesn’t mean the column can’t be NULL
```SQL
CREATE TABLE cats3  (    
    name VARCHAR(20) DEFAULT 'no name provided',    
    age INT DEFAULT 99  
);

INSERT INTO cats3() VALUES();


CREATE TABLE cats4  (    
    name VARCHAR(20) NOT NULL DEFAULT 'unnamed',    
    age INT NOT NULL DEFAULT 99 
);
```

### primary key
the unique identifer
```SQL
CREATE TABLE unique_cats (
	cat_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL
);

-- Another option:
CREATE TABLE unique_cats2 (
	cat_id INT,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    PRIMARY KEY (cat_id)
);
```

### auto increment
automatically generates a unique sequential number for a column (default is 1)
```SQL
CREATE TABLE unique_cats3 (
    cat_id INT AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL,
    PRIMARY KEY (cat_id)
);
```


### SELECT & WHERER
```SQL
SELECT name, breed FROM cats;


SELECT * FROM cats WHERE name ='Egg';

SELECT cat_id, age FROM cats WHERE cat_id=age;
```

### rename a column when print it out (temporary thing)

```SQL
SELECT cat_id AS id, name FROM cats;
```

### Update (UPDATE ... SET)
```SQL
UPDATE cats SET breed='Shorthair' WHERE breed='Tabby';
```

**try Select before you Update**
1. 確認資料存在
2. 有時條件不對 ,可能會更新到錯誤的資料

### delete(DELETE FROM)
```SQL
-- delete all cats with name of 'Egg'
DELETE FROM cats WHERE name='Egg';

-- delete all rows in the cats table
DELETE FROM cats;
```