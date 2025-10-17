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

# Case

根據不同條件，動態地決定某一欄位或運算的結果
CASE 可以讓查詢結果「有條件地改變」
=> CASE 讓 SQL 查詢能根據資料內容回傳不同值

舉個例子：
假設我們要查詢書名（title）和出版年份（released_year）
然後我們想要新增一個新的欄位叫做 genre（文學類別）
這個 genre 的值會根據出版年份來決定：

如果出版年份大於或等於 2000 年，就顯示 Modern Lit（現代文學）
否則（也就是 1900 年代的書）就顯示20th Century Lit（20 世紀文學）
```SQL
SELECT 
  title,
  released_year,
  CASE
    WHEN released_year >= 2000 THEN 'Modern Lit'
    ELSE '20th Century Lit'
  END AS genre
FROM books;
```

習慣先把 CASE 和 END 打好 => CASE 與 END 是成對使用的
然後在中間填入多組 WHEN ... THEN ... 條件 => 裡面可以有多個 WHEN ... THEN ... 條件
若都不成立，最後才會執行 ELSE => ELSE 是可選的，用來處理「其他情況」

最後記得用 AS genre 幫新欄位取個名字


#### 多層條件案例
根據書本的 庫存數量（stock_quantity） 來評分
用星號「*」來表示庫存多寡

```SQL
SELECT 
  title,
  stock_quantity,
  CASE
    WHEN stock_quantity BETWEEN 0 AND 40 THEN '*'
    WHEN stock_quantity BETWEEN 41 AND 70 THEN '**'
    WHEN stock_quantity BETWEEN 71 AND 100 THEN '***'
    WHEN stock_quantity BETWEEN 101 AND 140 THEN '****'
    ELSE '*****'
  END AS stock
FROM books;
```
很重要
- CASE 只會執行第一個為真的條件
- 如果第一個 WHEN 條件成立，就直接回傳那個值
- 如果不成立，就往下一個 WHEN 判斷
- 若都不成立，最後才會執行 ELSE

一種更簡潔的寫法
```SQL
SELECT 
  title,
  stock_quantity,
  CASE
   WHEN stock_quantity <= 40 THEN '*'
   WHEN stock_quantity <= 70 THEN '**'
   WHEN stock_quantity <= 100 THEN '***'
   WHEN stock_quantity <= 140 THEN '****'
    ELSE '*****'
  END AS stock
FROM books;
```