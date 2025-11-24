放在 OVER() 裡的 ORDER BY，跟我們之前看到的「一般的 ORDER BY」非常不同
它們相似之處是都會改變列（row）的順序
但當我們把 ORDER BY 放進 OVER() 的括號裡時
我們其實是在告訴 MySQL： 要在每一個 window（視窗區間）裡面重新調整列的順序

，當我們在某些聚合函數（例如 AVG 或 SUM）裡加上 ORDER BY 時，
它會產生 rolling average、rolling sum

```SQL
SELECT 
    emp_no, 
    department, 
    salary, 
    SUM(salary) OVER(PARTITION BY department ORDER BY salary) AS rolling_dept_salary,
    SUM(salary) OVER(PARTITION BY department) AS total_dept_salary
FROM employees;
 ```

rolling_dept_salary 如何算
| salary | 計算方式            | rolling_dept_salary |
| ------ | --------------- | ------------------- |
| 31,000 | 31,000          | 31,000          |
| 38,000 | 31,000 + 38,000 | 69,000          |
| 61,000 | 69,000 + 61,000 | 130,000         |




```SQL
SELECT 
    emp_no, 
    department, 
    salary, 
    MIN(salary) OVER(PARTITION BY department ORDER BY salary DESC) as rolling_min
FROM employees;
```

| salary | 目前看過的最小值               | rolling_min |
| ------ | ---------------------------- | ----------- |
| 31,000 | 31,000                       | 31,000  |
| 38,000 | min(31,000, 38,000) = 31,000 | 31,000  |
| 40,000 | min(31,000, 40,000) = 31,000 | 31,000  |
| 45,000 | min(31,000, 45,000) = 31,000 | 31,000  |
| 55,000 | min(31,000, 55,000) = 31,000 | 31,000  |
| 56,000 | min(31,000, 56,000) = 31,000 | 31,000  |
| 61,000 | min(31,000, 61,000) = 31,000 | 31,000  |

