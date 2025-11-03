# LEFT JOIN 「左邊的所有資料」＋「右邊有重疊的部分」
如果 customers 是左邊的表（left table） 
orders 是右邊的表（right table） 

那我們就會取出左邊表中所有的資料列 
也就是所有顧客（customers）
如果有對應的訂單資料 
就一起顯示
如果沒有，就會顯示一堆 NULL 值

```SQL
SELECT first_name, last_name, order_date, amount
FROM customers
LEFT JOIN orders
ON orders.customer_id = customers.id;
```

💡那為什麼我們要用 LEFT JOIN 呢？

因為它能顯示一些重要的資訊。

例如我想知道：

哪些顧客從來沒有下過訂單？

INNER JOIN 做不到，
因為它只顯示有訂單的顧客。

如果我只看 customers 表，也看不出來。

唯一的辦法是：
👉 把 customers 跟 orders 做 LEFT JOIN，
然後看哪些顧客在右邊（orders）是 NULL，
這樣就知道誰從來沒下過訂單


### 如果反過來呢？ 把 customers 和 order 對調
在「顧客：訂單 = 一對多」這種常見關係裡，
我們常會有「顧客沒下訂單」，但不太會有「訂單沒顧客」。

- 有顧客沒下單（常見）
- 但不太會有「訂單沒有顧客」的情況（不合理）

```SQL
SELECT ...
FROM orders
LEFT JOIN customers
ON customers.id = orders.customer_id;
```

那左邊變成 orders，右邊變成 customers。
我們重新排一下欄位順序讓它看起來「從左到右」。

執行這個查詢，你會發現結果跟 INNER JOIN 一樣。

為什麼呢？
因為在這個資料庫裡，
每筆 orders 都一定有對應的 customer_id。
也就是說，orders（左表）的每一筆都有匹配的顧客。