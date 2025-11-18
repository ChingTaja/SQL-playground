- HAVING
HAVING 可以理解成 對分組後的資料做條件篩選，跟 WHERE 類似，但有一個重要差別：
| 條件       | 用途                          | 例子                                           |
| -------- | --------------------------- | -------------------------------------------- |
| `WHERE`  | 在 **分組前** 篩選資料行（row-level）  | `WHERE rating > 3` → 只取評分大於 3 的行             |
| `HAVING` | 在 **分組後** 篩選分組（group-level） | `HAVING COUNT(rating) > 1` → 只保留評分數量大於 1 的電影 |

```SQL
SELECT 
    title, 
    AVG(rating) AS avg_rating,
    COUNT(rating) AS review_count
FROM full_reviews
WHERE rating >= 3         -- 篩掉評分小於 3 的單筆資料
GROUP BY title
HAVING COUNT(rating) > 1  -- 篩掉剩餘評分少於 2 筆的電影
ORDER BY avg_rating DESC;
```

```SQL
SELECT SUM(rating)
FROM full_reviews
HAVING SUM(rating) IS NOT NULL;
```
這裡的 HAVING 如果用 WHERE 代替呢？
會報錯, 因為WHERE 不能用聚合函數（COUNT、SUM、AVG …）
因為 WHERE 是在「分組前」就執行 , 而聚合函數只有在「分組後」才會知道結果