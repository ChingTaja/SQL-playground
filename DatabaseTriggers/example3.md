根據另一個動作」來產生新的資料

我們想記錄使用者何時取消追蹤別人（unfollow）

after delete（刪除後）

當 follows 表被刪除資料後
我們要自動在另一張不存在的表（叫 unfollows）新增一筆記錄


建立 Trigger
接著建立 trigger（另存成新的 .sql 檔）
```SQL
DELIMITER $$

CREATE TRIGGER create_unfollow
    AFTER DELETE ON follows FOR EACH ROW 
BEGIN
    INSERT INTO unfollows
    SET follower_id = OLD.follower_id,
        followee_id = OLD.followee_id;
END$$

DELIMITER ;
```