RANK() 只能用於 OVER，不能與 GROUP BY 搭配

RANK() 用來返回當前列在其 windows 內的排名

```SQL
SELECT 
    emp_no, 
    department, 
    salary, 
    RANK() OVER(PARTITION BY department ORDER BY salary) AS dept_salary_rank,
    RANK() OVER(ORDER BY salary DESC) as overall_salary_ranl
FROM employees ORDER BY department;
```

# DENSE_RANK & ROW_NUMBER

RANK 允許同排名（ties）：
例如兩筆資料都可以是第 1 名或第 4 名
因為有同排名，所以後續的排名數字可能==會被跳過==

ROW_NUMBER 則完全不管數值是否相同：
它只是單純對 partition 中的每一筆資料
依序從 1 開始編號：1、2、3、4、5...
不會因為同分而跳號，也不看值是否相同，只看列的順序

```SQL
SELECT 
    emp_no, 
    department, 
    salary,
    ROW_NUMBER() OVER(PARTITION BY department ORDER BY SALARY DESC) as dept_row_number,
    RANK() OVER(PARTITION BY department ORDER BY SALARY DESC) as dept_salary_rank,
    RANK() OVER(ORDER BY salary DESC) as overall_rank,
    DENSE_RANK() OVER(ORDER BY salary DESC) as overall_dense_rank,
    ROW_NUMBER() OVER(ORDER BY salary DESC) as overall_num
FROM employees ORDER BY overall_rank;
```