這個模式控制我們在使用 GROUP BY 的時候，可以選擇哪些欄位

規則：
1. 只能選擇聚合函數計算的欄位（如 AVG(), COUNT(), SUM()）
2. 只能選擇出現在 GROUP BY 子句中的欄位

2. 啟用模式

意思是說：如果 SELECT 的欄位列表中包含了"非聚合"欄位，就會拒絕執行查詢

- 正確範例
可以 `Select`：
1. title（在 GROUP BY 中）
2. AVG(rating)（聚合函數）

```SQL
SELECT title, AVG(rating)
FROM series
JOIN reviews
ON reviews.series_id = series.id
GROUP BY title;
```

-錯誤範例
```SQL
SELECT title, rating
FROM series
JOIN reviews
ON reviews.series_id = series.id
GROUP BY title;
```
問題：rating 不是聚合欄位，也沒出現在 GROUP BY 中
原因：SQL 不知道該選哪一個 rating（可能每個 title 有多個 rating）
SQL 執行時會報錯：
```Expression #2 of SELECT list is not in GROUP BY clause and contains non-aggregated column.```

如果關閉 ONLY FULL GROUP BY
會取每組的「第一個 rating」，而不是平均值。
所以建議 仍使用 ONLY FULL GROUP BY，避免結果誤解。