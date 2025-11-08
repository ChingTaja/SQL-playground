View 就是一個「查詢（query）」的結果
我們幫它取一個名字，然後把它「存起來」
以後就不用每次都重複打一大串查詢

當我們「呼叫」這個 view（也就是執行或查看它），
我們會看到這個查詢的結果，
而且它看起來就像一張真的資料表，
但其實不是——它是一張虛擬表（virtual table）

直接建立一個 view（檢視表）
取名為 full_reviews
```SQL
CREATE VIEW full_reviews AS
SELECT
  title,
  release_year,
  genre,
  rating,
  first_name,
  last_name
FROM reviews
JOIN series
  ON series.id = reviews.series_id
JOIN reviewers
  ON reviewers.id = reviews.reviewer_id;
```

可以用這張 virtual table 執行指令
```SQL
SELECT * FROM full_reviews
WHERE genre = 'Animation';
```