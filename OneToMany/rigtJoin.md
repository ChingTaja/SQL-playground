取出右表全部資料 + 能對上的左表資料

```SQL
SELECT c.name, o.amount
FROM customers c
RIGHT JOIN orders o
ON c.id = o.customer_id;
```
左邊表（Left Table）：customers
右邊表（Right Table）：orders