- DATEDIFF 計算兩個日期之間的天數差
- DATE_ADD 在指定日期上加上某個時間間隔
- DATE_SUB

```SQL
SELECT DATEDIFF('2025-10-10', '2025-10-01') AS days_diff;

DATE_ADD(date, INTERVAL value unit)
-- unit 可以是：DAY、MONTH、YEAR、HOUR、MINUTE、SECOND 等

SELECT DATE_SUB('2025-10-10', INTERVAL 5 DAY) AS new_date;
```
