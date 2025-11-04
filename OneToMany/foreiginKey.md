```SQL
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(50)
);
 
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    amount DECIMAL(8,2),
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
 
INSERT INTO customers (first_name, last_name, email) 
VALUES ('Boy', 'George', 'george@gmail.com'),
       ('George', 'Michael', 'gm@gmail.com'),
       ('David', 'Bowie', 'david@gmail.com'),
       ('Blue', 'Steele', 'blue@gmail.com'),
       ('Bette', 'Davis', 'bette@aol.com');
       
       
INSERT INTO orders (order_date, amount, customer_id)
VALUES ('2016-02-10', 99.99, 1),
       ('2017-11-11', 35.50, 1),
       ('2014-12-12', 800.67, 2),
       ('2015-01-03', 12.50, 2),
       ('1999-04-11', 450.25, 5);
```


### foreign keys and deletion

現在我們有兩張表：

一張是 customers（顧客）
一張是 orders（訂單）
每一筆訂單（order）都有一個 外鍵 customer_id

我們可以有「顧客沒有訂單」，這是合法的情況。
例如：剛註冊但還沒下單的顧客。

但問題是：

當我們刪除一位顧客時，應該發生什麼事？

```SQL
-- 報錯
-- “Cannot delete or update that parent row: a foreign key constraint fails”
-- 你不能刪除這筆「父表（parent）」資料
-- 因為子表（orders）裡還有引用這筆 customer_id 的資料

DELETE FROM customers
WHERE last_name = 'George';
```

原本建立 orders 表時，是這樣設定外鍵：
```SQL
FOREIGN KEY (customer_id) REFERENCES customers(id)
```

加上 ON DELETE CASCADE
==> 當 customers 表中某個顧客被刪除時，
所有在 orders 表中擁有相同 customer_id 的訂單也會自動被刪除。
```SQL
FOREIGN KEY (customer_id) REFERENCES customers(id)
ON DELETE CASCADE;
```