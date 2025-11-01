1. one to one

2. one to many
review < ---> book
對 review 來說只會對應到一本 book
對 book 來說可以對應到很多 review

3. many to many
book < ---> author
對 review 來說可以對應到多位 author
對 author 來說可以對應到很多 book


分開兩張表，用關聯欄位連接

customers
| id | first_name | last_name | email                                       |
| -- | ---------- | --------- | ------------------------------------------- |
| 1  | Boy        | George    | [george@gmail.com](mailto:george@gmail.com) |
| 2  | George     | Michael   | [gm@gmail.com](mailto:gm@gmail.com)         |
| 3  | David      | Bowie     | [david@gmail.com](mailto:david@gmail.com)   |
| 4  | Blue       | Steele    | [blue@gmail.com](mailto:blue@gmail.com)     |


orders
| id | order_date | amount | customer_id |
| -- | ---------- | ------ | ----------- |
| 1  | 2016-02-10 | 99.99  | 1           |
| 2  | 2017-03-15 | 35.50  | 1           |
| 3  | 2014-01-05 | 800.67 | 2           |
| 4  | 2015-05-22 | 12.50  | 2           |

這裡：
customer_id 在 orders 表中是外鍵（foreign key），
代表這筆訂單屬於哪一位顧客。

每位顧客在 customers 表中都有一個唯一的 id（主鍵 primary key）。

🧩 主鍵（Primary Key）

主鍵的用途是：

唯一識別表中的一列（row）。

不能重複。

通常會設為 AUTO_INCREMENT，自動編號。

```SQL
id INT AUTO_INCREMENT PRIMARY KEY
```

🧩 外鍵（Foreign Key）

外鍵是用來：

在一張表中「引用另一張表」的欄位。

在這個例子：

orders.customer_id 是外鍵，指向 customers.id

例如，如果你不小心新增：
```SQL
INSERT INTO orders (order_date, amount, customer_id)
VALUES ('2020-05-01', 50.00, 20);
```

但 customers 表裡根本沒有 id = 20 的顧客，
那這就造成「孤兒資料（orphan record）」。

所以在資料表定義時，可以這樣明確設置：
```SQL
FOREIGN KEY (customer_id) REFERENCES customers(id)
```

這樣資料庫會自動檢查，若對應不到，就會報錯