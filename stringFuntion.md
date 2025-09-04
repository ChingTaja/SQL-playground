- concat / concat with separator
```SQL
SELECT CONCAT(author_fname,' ', author_lname) AS author_name FROM books;

SELECT CONCAT_WS('-',title, author_fname, author_lname) FROM books;
```

- substirng -> pick a. portion of string (SUBSTR is same as SUBSTRING)
```SQL
SELECT SUBSTRING('Hello World', 1, 4);

SELECT SUBSTRING('Hello World', 7);
 
SELECT SUBSTRING('Hello World', -3);
 
SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;
 
SELECT SUBSTR(title, 1, 10) AS 'short title' FROM books;
```

- combine two method
```SQL
SELECT CONCAT
    (
        SUBSTRING(title, 1, 10),
        '...'
    ) AS 'short title'
FROM books;
```

- replace (replace with some string) ==> case-sensitive !!
```SQL
SELECT REPLACE('HellO World', 'o', '*');
```

- reverse 
```SQL
SELECT REVERSE(author_fname) FROM books;
```

- return bytes
```SQL
SLEECT LENGTH('hey!')
```
- return character length
```SQL
SELECT author_lname, CHAR_LENGTH(author_lname) AS 'length' FROM books;
```

- lower case / upper case
```SQL
SELECT UPPER('Hello World');
 
SELECT LOWER('Hello World');
```


```SQL
SELECT INSERT('Hello Bobby', 6, 0, 'There');
 
-- leftmost , rightmost
SELECT LEFT('omghahalol!', 3);

SELECT RIGHT('omghahalol!', 4);

SELECT REPEAT('ha', 4);

SELECT TRIM('  pickle  '); --LEADING / TAILING / BOTH
```
- refining selection

```SQL
-- 只有當 author_fname 和 author_lname 同時相同 時，才會被視為重複並去掉
SELECT DISTINCT author_fname, author_lname FROM books;  
 
SELECT DISTINCT CONCAT(author_fname,' ', author_lname) FROM books;
```

- order
```SQL
SELECT * FROM books ORDER BY released_year;

-- 這裡的 2 代表 SELECT 清單中的第二個欄位
SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY 2 desc;

-- 先排序 author_lname 再排序 author_fname
SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY author_lname, author_fname;
```