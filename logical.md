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

```SQL
-- compare date
SELECT * FROM people WHERE birthtime 
BETWEEN CAST('12:00:00' AS TIME) 
AND CAST('16:00:00' AS TIME);

SELECT * FROM people WHERE HOUR(birthtime)
BETWEEN 12 AND 16;
```

```SQL
-- in option
SELECT title, author_lname FROM books
WHERE author_lname = 'Carver' 
OR author_lname = 'Lahiri'
OR author_lname = 'Smith';

SELECT title, author_lname FROM books
WHERE author_lname IN ('Carver', 'Lahiri', 'Smith');

SELECT title, author_lname FROM books
WHERE author_lname NOT IN ('Carver', 'Lahiri', 'Smith');


SELECT title, released_year FROM books
WHERE released_year >= 2000 
AND released_year % 2 = 1;
```