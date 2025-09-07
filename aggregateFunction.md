- COUNT ( How many count in that column )

```SQL
SELECT COUNT(*) FROM books;
 
SELECT COUNT(author_lname) FROM books;
 
SELECT COUNT(DISTINCT author_lname) FROM books;
 
SELECT COUNT(*) FROM books WHERE title LIKE '%the%';
```