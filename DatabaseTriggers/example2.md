問題有很多解決方式
不一定要用資料庫來處理，也可以在 client-side 或 application-side 處理

接下來我們想做的是：防止使用者追蹤自己

```SQL
DELIMITER $$

CREATE TRIGGER example_cannot_follow_self
     BEFORE INSERT ON follows FOR EACH ROW
     BEGIN
          IF NEW.follower_id = NEW.following_id
          THEN
               SIGNAL SQLSTATE '45000'
                    SET MESSAGE_TEXT = 'Cannot follow yourself, silly';
          END IF;
     END;
$$

DELIMITER ;
```

接著執行：source ig.sql