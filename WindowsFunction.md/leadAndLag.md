它們最常被用來做比較——例如比較當前列與前一列、下一列之間的差異

若使用 LAG，回傳「同一個視窗內、上一列」該表達式的值

若使用 LEAD，回傳「同一個視窗內、下一列」該表達式的值

你也可以讓 LAG/LEAD 回傳「前 n 列」或「後 n 列」：
```SQL
LAG(salary, 2)
```

```SQL
SELECT 
    emp_no, 
    department, 
    salary,
    salary - LAG(salary) OVER(PARTITION BY department ORDER BY salary DESC) as dept_salary_diff
FROM employees;
```

