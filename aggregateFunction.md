- COUNT ( How many count in that column )

```SQL
SELECT COUNT(*) FROM books;
 
SELECT COUNT(author_lname) FROM books;
 
SELECT COUNT(DISTINCT author_lname) FROM books;
 
SELECT COUNT(*) FROM books WHERE title LIKE '%the%';
```

- GROUP BY 以...作為分類

![alt text](<截圖 2025-09-10 晚上11.12.25.png>)

注意：SELECT 中除了聚合函數以外的欄位 必須出現在 GROUP BY 裡面
```SQL
SELECT author_lname, COUNT(*) 
FROM books
GROUP BY author_lname;
 
SELECT 
    author_lname, COUNT(*) AS books_written
FROM
    books
GROUP BY author_lname
ORDER BY books_written DESC;
```

- max / min
```SQL
SELECT MAX(pages) FROM books;
 
SELECT MIN(author_lname) FROM books;
```

- subquery
```SQL
SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books)
```

-  方法Ａ `SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books)`
和  方法Ｂ`SELECT MIN(pages) FROM books` 有什麼差別
子查詢 (SELECT MAX(pages) FROM books) 會先找出 books 表中最大的頁數。

方法Ａ
外層查詢再選出 所有擁有最大頁數的書（可能不只一本，如果有多本書頁數一樣多）
👉 結果會包含 書名 (title) + 頁數 (pages)

方法Ｂ
這個只會回傳 一個數值 → 整張表中最小的頁數
不會顯示是哪本書