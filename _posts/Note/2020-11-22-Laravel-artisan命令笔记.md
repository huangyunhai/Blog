---
layout: post
category: Note
tags: root
---
1. 数据库迁移文件
```sh
# 创建迁移文件
php artisan make:migration create_users_table
# 执行迁移（建表）
php artisan migrate
```