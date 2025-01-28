主要是 [FoF Upload](https://github.com/FriendsOfFlarum/upload/issues/426) 默认添加的是绝对url，因此需要统一修改。以从`https://flarum.example.com`到`https://flarum.example.net`为例：

1. 备份数据库
```sh
mysqldump -u flarum_user -p flarum_db > flarum_backup.sql
```
2. 批量替换
```sql
START TRANSACTION;
UPDATE flarum_db.post_edit_histories 
SET content = REPLACE(
    content,
    'https://flarum.example.com',
    'https://flarum.example.net'
)
WHERE content LIKE '%https://flarum.example.com%';
UPDATE flarum_db.posts
SET content = REPLACE(
    content,
    'https://flarum.example.com',
    'https://flarum.example.net'
)
WHERE content LIKE '%https://flarum.example.com%';
COMMIT;
```
3. 删去`/storage/cache`缓存