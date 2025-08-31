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