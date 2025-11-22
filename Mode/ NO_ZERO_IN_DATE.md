NO_ZERO_IN_DATE
NO_ZERO_DATE
這兩個模式主要控制 日期中的零值 (0)

1️⃣ NO_ZERO_IN_DATE

控制 日期欄位中日或月不能為 0

允許年份存在，但 月或日為 0 會產生警告或錯誤（依嚴格模式而定）

ex：

'2010-00-01'  -- 月份為 0 → 不允許
'2010-01-00'  -- 日為 0 → 不允許
'2010-01-15'  -- 有效日期 → 允許

2️⃣ NO_ZERO_DATE

控制 整個日期欄位不能是全零（'0000-00-00'）。

也就是不允許日期為零日期（零年、零月、零日）。

例子：

'0000-00-00'  -- 完全零日期 → 不允許
'2010-01-15'  -- 有效日期 → 允許
'2010-01-00'  -- 僅日為 0 → NO_ZERO_DATE 不會阻止，但 NO_ZERO_IN_DATE 會


還有第三種情況：「如果此模式和嚴格模式都啟用」，則會產生 錯誤（error）


嚴格模式 (STRICT_TRANS_TABLES) 影響 INSERT/UPDATE 的行為。
- NO_ZERO_IN_DATE + 非嚴格模式 → 警告，允許零日期(仍會插入日期)
- NO_ZERO_IN_DATE + 嚴格模式 → 錯誤，不允許零日期
```SQL
INSERT INTO dates (D) VALUES ('2023-11-00');
```

什麼是嚴格模式（strict mode）？

當啟用以下任一模式時，嚴格模式會生效：

1.STRICT_ALL_TABLES

2.STRICT_TRANS_TABLES

而 STRICT_TRANS_TABLES 是 預設啟用 的