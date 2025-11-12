修改 View 的內容
方法一：CREATE OR REPLACE VIEW

語法：

```SQL
CREATE OR REPLACE VIEW view_name AS
SELECT ...;
```

功能：
- 若 view 不存在 → 建立新 view
- 若 view 已存在 → 以新內容取代舊 view

常用情境：
- 欄位名稱改變（例如 released_year → year）

- 查詢邏輯需要更新（排序方式、JOIN 條件等）

✅ 範例：

```SQL
CREATE VIEW ordered_series AS
SELECT * FROM series ORDER BY released_year;

CREATE OR REPLACE VIEW ordered_series AS
SELECT * FROM series ORDER BY released_year DESC;
```

方法二：ALTER VIEW

語法：
```SQL
ALTER VIEW view_name AS
SELECT ...;
```

功能：

- 直接用新的查詢內容更新現有 view

- 效果與 CREATE OR REPLACE VIEW 類似

- 寫法更「語意化」（像是「修改現有的 view」）

🗑️ 3️ 刪除 View

語法：
```SQL
DROP VIEW view_name;
```

只會刪除 view 本身，不會刪除原始資料表。

範例：
```SQL
DROP VIEW ordered_series;
```