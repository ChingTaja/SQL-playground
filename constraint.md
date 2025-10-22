#### UNIQUE
保證某個欄位（或一組欄位）的值在資料表中 不會重複 的約束條件
```SQL
CREATE TABLE contacts (
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(15) NOT NULL UNIQUE
);
 
INSERT INTO contacts (name, phone)
V   LUES ('billybob', '8781213455');
 
-- This insert would result in an error:
INSERT INTO contacts (name, phone)
VALUES ('billybob', '8781213455');
```

#### CHECK
- 限制欄位值必須符合特定條件 的約束（constraint），確保資料表中的資料符合規則
```SQL
CREATE TABLE users (
    username VARCHAR(20) NOT NULL,
    age INT CHECK (age > 0)
);
 
CREATE TABLE palindromes (
    word VARCHAR(100) CHECK(REVERSE(word) = word)
)
```

#### name the constraint (CONSTRAINT)
1. it is good for read and check

```SQL
CREATE TABLE users2 (
    username VARCHAR(20) NOT NULL,
    age INT,
    CONSTRAINT age_not_negative CHECK (age >= 0)
);

CREATE TABLE palindromes2 (
  word VARCHAR(100),
  CONSTRAINT word_is_palindrome CHECK(REVERSE(word) = word)
);
```