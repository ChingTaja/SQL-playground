
- WITH ROLLUP

GROUP BY 一起使用的子句：WITH ROLLUP

案例：每月水果銷售總額

假設我們有一個 sales 表：
| month | product | amount |
| ----- | ------- | ------ |
| Jan   | Apple   | 100    |
| Jan   | Banana  | 150    |
| Feb   | Apple   | 120    |
| Feb   | Banana  | 130    |

我們想要：

1.每個月每種水果銷售額

2.每月小計

3.全部總計

```SQL
SELECT month, product, SUM(amount) AS total_sales
FROM sales
GROUP BY month, product WITH ROLLUP;
```


結果
| month | product | total_sales     |
| ----- | ------- | --------------- |
| Jan   | Apple   | 100             |   ------>  month + product
| Jan   | Banana  | 150             |
| Jan   | NULL    | 250   ← Jan 月小計 |  ------>  only month
| Feb   | Apple   | 120             |
| Feb   | Banana  | 130             | 
| Feb   | NULL    | 250   ← Feb 月小計 | 
| NULL  | NULL    | 500   ← 全年總計    |  ------>  SUM (250 + 250)


🔹 對應公式理解

每個組（month + product）：
SUM(amount) WHERE month=? AND product=?


每個月小計：
SUM(amount) WHERE month=?  (不分 product)


全部總計：
SUM(amount) OVER ALL