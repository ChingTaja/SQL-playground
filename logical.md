```SQL
-- not equal
SELECT * FROM books
WHERE released_year != 2017
```

```SQL
-- not like
SELECT * FROM books
WHERE title NOT LIKE '%e%';
```

```SQL
-- greater than
SELECT * FROM books
WHERE released_year > 2005;

-- less than
SELECT * FROM books
WHERE released_year < 2000;
 
SELECT * FROM books
WHERE released_year <= 1985;
```

```SQL
-- &&
SELECT title, author_lname, released_year FROM books
WHERE released_year > 2010
AND author_lname = 'Eggers'
AND title LIKE '%novel%';

-- or
SELECT title, pages FROM books
WHERE pages < 200 
OR title LIKE '%stories%';

-- between
SELECT title, released_year FROM books
WHERE released_year BETWEEN 2004 AND 2014;

-- not between
SELECT title, released_year FROM books
WHERE released_year NOT BETWEEN 2004 AND 2014;
```

### CAST(值 AS 資料型別)
某個值轉換成指定的型別
```SQL
-- compare date
SELECT * FROM people WHERE HOUR(birthtime) > 12 

SELECT * FROM people WHERE birthtime 
-- '12:00:00' 原本是 字串（string） 
CAST('12:00:00' AS TIME) -- → 把它轉成 時間型別 (TIME)
BETWEEN CAST('12:00:00' AS TIME) 
AND CAST('16:00:00' AS TIME);

SELECT * FROM people WHERE HOUR(birthtime)
BETWEEN 12 AND 16;
```


```SQL
-- 假如我要查 100 位作者的話，這樣就得寫一大串 很麻煩
SELECT title, author_lname FROM books
WHERE author_lname = 'Carver' 
OR author_lname = 'Lahiri'
OR author_lname = 'Smith';

-- in option
-- 是否「在某一組指定的值之中」
SELECT title, author_lname FROM books
WHERE author_lname IN ('Carver', 'Lahiri', 'Smith');

-- 找出「不是 Carver、Lahiri 或 Smith」的作者
SELECT title, author_lname FROM books
WHERE author_lname NOT IN ('Carver', 'Lahiri', 'Smith');
```
```SQL
-- 選出那些出版年份不是偶數
SELECT title, released_year FROM books
WHERE released_year >= 2000 
AND released_year % 2 = 1;
```