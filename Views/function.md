
- WITH ROLLUP

GROUP BY 一起使用的子句：WITH ROLLUP


假設我們使用：
```SQL
SELECT * FROM full_reviews;
```

這是一個 view（資料視圖），把三個資料表 join 在一起

接著我們用其中一個聚合函數，例如 AVG() 或 COUNT()

✔ 整張表的平均評分
```SQL
SELECT AVG(rating) FROM full_reviews;
```
這會給我們整張表的平均值

✔ 按 title 分組的平均評分
```SQL
SELECT title, AVG(rating)
FROM full_reviews
GROUP BY title;
```

同樣是 AVG()，但現在作用在「每一組」，也就是每個 title 上面。

🔹 使用 WITH ROLLUP

現在，如果我們在上一個查詢後面加上：
```SQL
GROUP BY title WITH ROLLUP;
```

結果看起來幾乎一樣，但會多出最後一列：

最後一列的 title 是 NULL

它代表 整張表的總平均