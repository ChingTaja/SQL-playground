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

Views 可能看起來像一個表格
在某些情況下它們就像表格一樣
但實際上它們背後並不是真正的表格。這就意味著，我們不能對 view 執行所有表格操作

如果這是一個真正的表格，我可以這樣做：刪除某些資料。
例如，我想刪除 2010 年發行的所有資料。
對一個普通表格，我會寫：

```SQL
delete from full_reviews
where released_year = 2010;
```

但是對 view 就行不通，它會告訴我： cannot delete from join view called full_reviews

不同類型的 view 有不同規則，可能會很複雜，官方文件有一整頁講解這個問題。基本上，只有極少部分的 view 是可以更新（updatable）和插入（insertable）的