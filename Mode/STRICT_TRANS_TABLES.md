「Trans」代表 transactional（交易性的），
而這個模式在 MySQL 中預設應該是啟用的(MySQL 8 之後，預設會啟用 strict trans tables)

如果執行：
```SQL
SELECT @@global.sql_mode;
```
你會看到 STRICT_TRANS_TABLES

Strict mode 控制 MySQL 在執行資料變更語句（例如 INSERT 或 UPDATE）時，
如何處理「無效」或「缺失」的值

我們有一個之前建立的 reviews 表

rating 是 decimal
我現在只插入 rating，
但我要插入一個字串（例如："hi"）。

INSERT INTO reviews (rating) VALUES ('hi');


會發生什麼？
→ 它 沒有被插入。
→ MySQL 丟出 完整的錯誤：

```SQL
Incorrect decimal value: 'hi' for column rating
```

這是一個完整的錯誤，所以 INSERT 失敗

若關閉這個模式
1. 行為會執行 （值會被插入）
2. 爆出警告 （`SHOW WARNINGS`）
