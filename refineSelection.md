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

- limit (starting row, count you want to retrieve)
```SQL
SELECT title, released_year FROM books ORDER BY released_year DESC LIMIT 10,1;

--即使資料表中沒有足夠的資料，也不會報錯。它只是會返回實際存在的資料數量。
SELECT * FROM tbl LIMIT 95,18446744073709551615;
```

- LIKE and wildcard
```SQL
-- % 代表 任意長度的字串（0 個或多個字
SELECT name FROM users WHERE name LIKE '%da%';

-- _（底線) 代表一個字元
SELECT * FROM books WHERE author_fname LIKE '____';
SELECT * FROM books WHERE author_fname LIKE '_a_';
```

- escaping wildcard
```SQL
-- To select books with '%' in their title:
SELECT * FROM books WHERE title LIKE '%\%%';
 
-- To select books with an underscore '_' in title:
SELECT * FROM books WHERE title LIKE '%\_%';
```