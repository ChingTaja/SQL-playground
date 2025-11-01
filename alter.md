- add column
```SQL
ALTER TABLE companies 
ADD COLUMN phone VARCHAR(15);
 
ALTER TABLE companies
ADD COLUMN employee_count INT NOT NULL DEFAULT 1;
```

- drop column
```sql
ALTER TABLE companies DROP COLUMN phone;
```

- rename
```sql
RENAME TABLE companies to suppliers; 

ALTER TABLE suppliers RENAME TO companies; 

ALTER TABLE companies RENAME COLUMN name TO company_name;
```

- modify column definition
```sql
-- 修改 欄位屬性（定義），但不改欄位名稱
ALTER TABLE companies
MODIFY company_name VARCHAR(100) DEFAULT 'unknown';

-- 改欄位名稱與屬性
ALTER TABLE suppliers
CHANGE business biz_name VARCHAR(50);
```


- ALTER TABLE + ADD CONSTRAINT
- 在 houses 資料表中，新增一個檢查約束（check constraint）
```SQL
ALTER TABLE houses
-- positive_p_price 是 constraint 的名稱
ADD CONSTRAINT positive_p_price
CHECK (purchase_price >= 0);

-- 驗證
INSERT INTO houses (purchase_price, sale_price)
VALUES (-1, 4);
```

- ALTER TABLE + DROP CONSTRAINT 
- 刪除約束（Drop Constraint）
```SQL
ALTER TABLE houses
DROP CONSTRAINT positive_p_price;
```