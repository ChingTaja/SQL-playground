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