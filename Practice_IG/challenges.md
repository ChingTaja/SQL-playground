# 1 finding 5 oldest user

```SQL
SELECT * FROM users
ORDER BY created_at
LIMIT 5;
```

# 2 what day of week do user register on ?

```SQL
SELECT 
    DAYNAME(created_at) AS day,
    COUNT(*) AS total
FROM users
GROUP BY day
ORDER BY total DESC
```

# 3 usesr with no photos
using left join
```SQL
SELECT username
FROM users
LEFT JOIN photos
    ON users.id = photos.user_id
WHERE photos.id IS NULL;
```
# 4 find most popular photo and who create it
- every like has its own data
```SQL
SELECT 
    username,
    photos.id,
    photos.image_url, 
    COUNT(*) AS total
FROM photos
INNER JOIN likes
    ON likes.photo_id = photos.id
INNER JOIN users
    ON photos.user_id = users.id
GROUP BY photos.id
ORDER BY total DESC
LIMIT 1;
```

# 5 calculate  avg number of photos per users

=> total number of photo / total number of users
一個查詢最終必須是 SELECT ... 開頭，並輸出一個結果
```SQL
SELECT (SELECT Count(*) 
        FROM   photos) / (SELECT Count(*) 
                          FROM   users) AS avg; 
```

# 6 top5 most commonly used tag
一個標籤被使用的 次數 ——這必須從 photo_tags（photos 與 tags 的中介表）計算
```SQL
SELECT tags.tag_name, 
       Count(*) AS total 
FROM   photo_tags 
       JOIN tags 
         ON photo_tags.tag_id = tags.id 
GROUP  BY tags.id 
ORDER  BY total DESC 
LIMIT  5; 
```

# 7 finding bots - user who have liked every single photo
```SQL
SELECT username, 
       Count(*) AS num_likes 
FROM   users 
       INNER JOIN likes 
               ON users.id = likes.user_id 
GROUP  BY likes.user_id 
HAVING num_likes = (SELECT Count(*) 
                    FROM   photos); 
```
