方案 1 一個 table 單一欄位儲存

- tags
| id | caption | tags                  |
| -- | ------- | --------------------- |
| 1  | 我的貓     | cute#cat#pets         |
| 2  | 午餐      | food#microwave#gross  |
| 3  | 自拍      | selfie#smile#ego#cute |


缺點：
1. tags 數量受字串長度限制
2. 無法儲存額外資訊（如第一次使用時間）
3. 搜尋要小心避免誤抓，例如 %food% 會抓到 sadfood

方案 2 兩個 table

- photos table
| id | caption |
| -- | ------- |
| 1  | 我的貓     |
| 2  | 午餐      |
| 3  | 自拍      |

- tags table
| id | photo_id | tag_name  |
| -- | -------- | --------- |
| 1  | 1        | cute      |
| 2  | 1        | cat       |
| 3  | 1        | pets      |
| 4  | 2        | food      |
| 5  | 2        | microwave |
| 6  | 2        | gross     |
| 7  | 3        | selfie    |
| 8  | 3        | smile     |
| 9  | 3        | ego       |
| 10 | 3        | cute      |

優點：

1. tags 數量無限制
2. 一個標籤可以對應多張照片

缺點：
1. 標籤名稱會重複儲存
2. 插入、更新、刪除效率低於方案一

方案 3 三個 table

- photos table
| id | caption |
| -- | ------- |
| 1  | 我的貓     |
| 2  | 午餐      |
| 3  | 自拍      |

- tags table
| id | tag_name  |
| -- | --------- |
| 1  | cute      |
| 2  | cat       |
| 3  | pets      |
| 4  | food      |
| 5  | microwave |
| 6  | gross     |
| 7  | selfie    |
| 8  | smile     |
| 9  | ego       |


-  photo_tags table (中間 table)
| photo_id | tag_id |
| -------- | ------ |
| 1        | 1      |
| 1        | 2      |
| 1        | 3      |
| 2        | 4      |
| 2        | 5      |
| 2        | 6      |
| 3        | 7      |
| 3        | 8      |
| 3        | 9      |
| 3        | 1      |

優點：

1. tags 數量無限制
 
2. 標籤重複儲存少

3. 可儲存額外資訊，如標籤首次使用時間、每次使用時間、地點等

缺點：

1. 插入、更新、刪除操作較複雜

2. 刪除標籤要注意中間表的孤兒資料


最終選擇方案二
```SQL
CREATE TABLE tags (
  id INTEGER AUTO_INCREMENT PRIMARY KEY,
  tag_name VARCHAR(255) UNIQUE,
  created_at TIMESTAMP DEFAULT NOW()
);
CREATE TABLE photo_tags (
    photo_id INTEGER NOT NULL,
    tag_id INTEGER NOT NULL,
    FOREIGN KEY(photo_id) REFERENCES photos(id),
    FOREIGN KEY(tag_id) REFERENCES tags(id),
    PRIMARY KEY(photo_id, tag_id)
);
```