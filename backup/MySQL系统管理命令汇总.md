- 创建数据库，设定数据库字符集为utf8mb4
```
CREATE DATABASE db_name DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE DATABASE db_name DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```
- 设定数据库字符集为gbk，名称为mydb2
```
CREATE DATABASE db_name DEFAULT CHARACTER SET gbk COLLATE gbk_chinese_ci;
```
- 更改数据库的字符编码
```
ALTER DATABASE db_name DEFAULT CHARACTER SET gbk  COLLATE gbk_chinese_ci;
```