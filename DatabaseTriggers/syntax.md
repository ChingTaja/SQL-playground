這是 SQL 語句
一些在特定事件發生時會「自動執行」的程式碼
只要某個資料表發生了變化，就會觸發它

```SQL
CREATE TRIGGER trigger_name 
    trigger_time trigger_event ON table_name FOR EACH ROW
    BEGIN
    ...
    END;
```

# The Syntax
trigger_time
- BEFORE
- AFTER

trigger_event
- INSERT
- UPDATE
- DELETE
- ON

table_name
- photos
- users


# 使用情境

紀錄歷史或操作其他表 , 紀錄歷史（logging history）。 

例如：

在社群網站裡，有追蹤（follow）紀錄。
假設你想知道「某人什麼時候取消追蹤某人」——
但如果使用者刪除追蹤紀錄，資料就直接消失了。

那你可以用 trigger：

在 follow 被刪除的「之後」
自動新增一筆紀錄到另一張表
例如 unfollows_log。