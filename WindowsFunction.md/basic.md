window function = 聚合 + 視窗

精髓：在保留原始資料的同時，計算出群組相關的值

假設我們有一個員工表（employees table），只有四列資料：

員工編號（employee ID）

所屬部門（department）

薪水（salary）

資料如下：
| employee_id | department       | salary |
| ----------- | ---------------- | ------ |
| 1           | Sales            | 60000  |
| 2           | Sales            | 59000  |
| 3           | Customer Service | 55000  |
| 4           | Customer Service | 56000  |

如果我們用 GROUP BY 部門計算平均薪水
會得到兩個群組： GROUP BY 會把每個群組的多列資料壓縮成一列
| department       | avg_salary |
| ---------------- | ---------- |
| Sales            | 59500      |
| Customer Service | 55500      |

而 視窗函數（Window Functions） 跟 GROUP BY 有點像，也可以對群組做聚合計算，
但最大的不同是：

視窗函數不會壓縮行數，而是對每一列都保留原始資料，並把計算結果附加在每一列旁邊

```SQL
SELECT
    employee_id,
    department,
    salary,
    AVG(salary) OVER(PARTITION BY department) AS dept_avg_salary
FROM employees;
```

| employee_id | department       | salary | dept_avg_salary |
| ----------- | ---------------- | ------ | --------------- |
| 1           | Sales            | 60000  | 59500           |
| 2           | Sales            | 59000  | 59500           |
| 3           | Customer Service | 55000  | 55500           |
| 4           | Customer Service | 56000  | 55500           |
