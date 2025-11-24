「會回傳視窗框架（window frame）中第一列的某個欄位值
```SQL
SELECT 
    emp_no, 
    department, 
    salary,
    FIRST_VALUE(emp_no) OVER(PARTITION BY department ORDER BY salary DESC) as highest_paid_dept,
    FIRST_VALUE(emp_no) OVER(ORDER BY salary DESC) as highest_paid_overall
FROM employees;
```

同設定下的行為
✔ 沒有 PARTITION BY → 整張表是一個視窗
```
FIRST_VALUE(employee_number) OVER (ORDER BY salary DESC)
```
- 全表按薪水排序
- 第一列 = 薪水最高的那一筆

所有列都會顯示同一個員工編號（最高薪的人）

✔ 有 PARTITION BY → 每個部門獨立排序
```
FIRST_VALUE(employee_number) 
OVER (PARTITION BY department ORDER BY salary DESC)
```
- 每個部門各自排序
- 每列會得到「該員工所屬部門的最高薪員工編號」