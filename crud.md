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