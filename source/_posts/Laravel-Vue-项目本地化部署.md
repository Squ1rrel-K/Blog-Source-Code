---
title: Laravel Vue 项目本地化部署
date: 2022-10-14 10:20:41
tags: coding
---

# 项目拷贝

```shell
git clone git@github.com:YourUserName/YourRepositories.git
```

# 本地化

```shell
composer install 
cp .env.example .env # Then modify .env file
php artisan key:generate
npm install
npm install vue-loader vue-template-compiler --save-dev
# modify webpack, add vue() to import chain
npm run dev
```
