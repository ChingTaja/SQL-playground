將資料依排序結果平均分成 N 個「桶」（buckets）
並回傳每筆資料落在第幾個桶：1 ~ N

1 = 表示最「前面的那一組」（依 ORDER BY 的方向決定）

N = 最後一組

每個 bucket 的資料量盡量平均

```SQL
SELECT 
    emp_no, 
    department, 
    salary,
    -- 各部門內部分成 4 組 (在 部門內 的薪資四分位)
    NTILE(4) OVER(PARTITION BY department ORDER BY salary DESC) AS dept_salary_quartile,
    -- 全公司依薪水分成 4 組 (在 整家公司 的薪資四分位)
    NTILE(4) OVER(ORDER BY salary DESC) AS salary_quartile
FROM employees;
```