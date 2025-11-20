SQL Mode 是一組「規則開關」，用來控制 MySQL 的語法行為與資料驗證方式。
開啟或關閉它們會讓 MySQL 的行為變得更嚴格，或更寬鬆

- 讓資料庫變得更嚴格、更安全，避免爛資料進入資料庫
- 增加語法一致性
- 跟其他資料庫相容

3. 模式有兩個作用範圍
🔹 Global（全域）

影響 所有使用者

影響 所有連線

若設成 Global → 永久生效（除非改回）

🔹 Session（當前連線）

只影響你現在這次連線

重新開 MySQL 會恢復預設



```SQL
-- To View Modes:
SELECT @@GLOBAL.sql_mode;
SELECT @@SESSION.sql_mode;
 
-- To Set Them:
SET GLOBAL sql_mode = 'modes';
SET SESSION sql_mode = 'modes';
```

| 模式                                 | 功能（白話）                             |
| ---------------------------------- | ---------------------------------- |
| **STRICT_TRANS_TABLES**            | 不讓你插入怪資料（例如格式不對），避免 silently 變成預設值 |
| **ONLY_FULL_GROUP_BY**             | GROUP BY 變更嚴格，避免結果不確定              |
| **NO_ZERO_DATE / NO_ZERO_IN_DATE** | 不准使用 0000-00-00 日期                 |
| **ERROR_FOR_DIVISION_BY_ZERO**     | 除以零時提醒/警告                          |
| **NO_ENGINE_SUBSTITUTION**         | 指定引擎不存在時不要自動換其他引擎                  |

6. 如何修改 SQL Mode？

你不能只「移除某一個模式」，
你必須 重新列出整串模式字串。

例如設定 Session SQL Mode：
```SQL
SET SESSION sql_mode = 'STRICT_TRANS_TABLES,NO_ZERO_IN_DATE';
```
要移除某個模式 → 在字串裡把它「拿掉」


 7. 範例：移除 ERROR_FOR_DIVISION_BY_ZERO

預設情況下：
```SQL
SELECT 3/0;
```
→ 會出現 warning：division by zero
若你重新設定 session SQL mode，不包含該模式：

```SQL
SET SESSION sql_mode = 'STRICT_TRANS_TABLES,ONLY_FULL_GROUP_BY,...';
```

再執行：
SELECT 3/0;
→ 不會有警告
→ 結果會是 NULL