- combine two different table


### inner join （INNER JOIN 是「內連接」的全名，但在 SQL 裡，JOIN 預設就是 INNER JOIN）

假設我們有兩個表：
一個是 customers，一個是 orders

如果我們執行：
```SQL
SELECT * FROM customers;
SELECT * FROM orders;
```

我們會看到每個訂單都有一個 customer_id 欄位，

如果我用人的直覺來找「誰下了這個訂單」，
我會看訂單裡的 customer_id，
然後回到顧客表裡找出相同 id 的人
```SQL
SELECT * FROM customers
JOIN orders
ON orders.customer_id = customers.id;
```

這裡 JOIN 後面要指定要連接的表（orders）
然後用 ON 來說明「怎麼連接」
也就是「哪個欄位要互相比對」

執行這個查詢之後，我們會得到：

左邊的欄位（id, first_name, last_name, email）來自 customers

右邊的欄位（id, order_date, amount, customer_id）來自 orders

如果資料太多，我們可以選擇只顯示部分欄位：
```SQL
SELECT first_name, last_name, order_date, amount
FROM customers
JOIN orders
ON orders.customer_id = customers.id;
```

我們也可以反過來： 結果是一樣的 順序不同而已
```SQL
SELECT * 
FROM orders
JOIN customers
ON customers.id = orders.customer_id;
```

| JOIN 類型    | 表順序是否影響結果？ | 說明               |
| ---------- | ---------- | ---------------- |
| INNER JOIN | ❌ 不影響      | 只取交集             |
| LEFT JOIN  | ✅ 影響       | 取左邊所有資料          |
| RIGHT JOIN | ✅ 影響       | 取右邊所有資料          |
| FULL JOIN  | ❌ 不影響      | 取聯集（但 MySQL 不支援） |


# inner join + group by
```SQL
SELECT 
    first_name, last_name, SUM(amount) AS total
FROM
    customers
        JOIN
    orders ON orders.customer_id = customers.id
GROUP BY first_name , last_name
ORDER BY total;
```