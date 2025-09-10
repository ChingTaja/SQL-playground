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