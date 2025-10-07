#### timestamp 和 datetime 的差異

 They both store datetime information, but there's a difference in the range, 

| 類型              | 範圍                                                                   |
| --------------- | -------------------------------------------------------------------- |
| **`DATETIME`**  | `'1000-01-01 00:00:00'` ～ `'9999-12-31 23:59:59'`                    |
| **`TIMESTAMP`** | `'1970-01-01 00:00:01' UTC` ～ `'2038-01-19 03:14:07' UTC`（32-bit 限制） |

timestamp 使用更少的儲存空間

儲存範圍： '1970-01-01 00:00:01' UTC ~ '2038-01-19 03:14:07' UTC
存入時：TIMESTAMP 會把你的本地時間 轉成 UTC 存進資料庫
讀取時：再把 UTC 轉回當前時區

```SQL
CREATE TABLE captions2 (
  text VARCHAR(150),
  created_at TIMESTAMP default CURRENT_TIMESTAMP,

-- 如果想讓資料在「每次被修改時」自動更新時間戳
  updated_at TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```