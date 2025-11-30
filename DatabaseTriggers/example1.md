```SQL
CREATE TABLE users (
  username VARCHAR(255),
  age INT
);
```

沒有 Trigger 時 , insert 未滿 18 歲的使用者 data 會成功
```SQL
INSERT INTO users (username, age) VALUES ('Sally', 16)
```

建立 Trigger 的語法
```SQL
DELIMITER $$

CREATE TRIGGER must_be_adult
     BEFORE INSERT ON users FOR EACH ROW
     BEGIN
          IF NEW.age < 18
          THEN
              SIGNAL SQLSTATE '45000'
                    SET MESSAGE_TEXT = 'Must be an adult!';
          END IF;
     END;
$$

DELIMITER ;
```
- BEFORE INSERT ON users
在插入到 users 表之前執行這段程式碼

- FOR EACH ROW
每插入一筆資料都會被檢查一次

- NEW.age
EW 在 trigger 裡是一個「替身」
他代表即將被插入的那一筆資料

NEW.age → 新插入的 age
OLD.age → 被更新前或刪掉前的 age

- SQLSTATE '45000'
    - 固定用來表示 自訂錯誤
    - 不屬於 MySQL 內建錯誤

- 為什麼需要 DELIMITER？
在 MySQL 中：
預設結束符號是分號 ;

MySQL 看到 ; 就會認為指令結束，立即執行

問題：
Trigger、Procedure、Function 裡面有很多分號，如果直接用分號 ;
MySQL 會把 trigger 誤認為多個單獨指令 → 建立失敗
改用自訂結束符號，常用 $$ <DELIMITER $$ → 暫時把結束符號改成 $$>