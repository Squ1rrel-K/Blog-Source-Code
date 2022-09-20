---
title: 基于 Ubuntu 的 Laravel 服务器部署
date: 2022-07-26 19:07:10
tags: coding
categories:
- 服务器部署

---

# 基本信息

服务器：百度云，2核/4GB内存/80GB磁盘/6Mbps带宽/Ubuntu ( ubuntu-20.04-amd64-20220507112023 ) 

Laravel：^7.0.1



## 操作系统选择

Debian，Centos 在 R 语言的部署上各有问题，选择 Ubuntu ( ubuntu-20.04-amd64-20220507112023 ) 



## 一. R 语言安装

[官方文档](https://cran.r-project.org/bin/linux/ubuntu/)



### 1. 获取最新版本的 R 语言

```shell
# 检查更新
$ sudo apt update -qq

# 安装 dirmngr - 软件证书的管理工具
$ sudo apt install --no-install-recommends software-properties-common dirmngr

# add the signing key (by Michael Rutter) for these repos
# To verify key, run gpg --show-keys /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc 
# Fingerprint: E298A3A825C0D65DFD57CBB651716619E084DAB9
$ wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc

# add the R 4.0 repo from CRAN -- adjust 'focal' to 'groovy' or 'bionic' as needed
$ sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
```



### 2. 安装 R 语言

```
# 安装 R 语言
$ sudo apt install --no-install-recommends r-base
```



### 3. 测试 R 语言

在此页面应能看到 R 的版本

```shell
# 打开 R 交互式窗口
$ R
```



## 二. 安装宝塔

[宝塔](https://www.bt.cn/new/index.html)是一个较为简单快捷的部署工具



### 1. 选择在线安装

记住给的服务器地址和登陆密码！

[![jzvfxg.png](https://s1.ax1x.com/2022/07/26/jzvfxg.png)](https://imgtu.com/i/jzvfxg)



### 2.  进入管理页面

(1) 选择 [软件商店]，一键安装 nginx 1.21.0，php-8

(2) 选择 [网站]，添加站点，域名为网站域名

(3) 选择 [软件商店]，php 设置，安装扩展，安装 fileinfo 插件，若报错 `Cannot find **auto**conf. Please check your autoconf installation and the $PHP_AUTOCONF environment variable. Then, rerun this script`

则运行

```shell
$ apt-get install autoconf -y
```

以安装

(4) 选择 [软件商店]，php 设置，删除以下被禁用的函数：

```php
putenv
pcntl_signal
proc_open
exec
```



## 三. 部署项目代码

```shell
# 进入目录，参数应与域名相符
$ cd /www/wwwroot/120.48.100.162

# clone 项目
$ git clone https://github.com/Squ1rrel-K/getLCAI_web.git

$ cd getLCAI_web
$ composer install

# 建立 .env 文件，生成密匙
$ php -r "file_exists('.env') || copy('.env.example', '.env');"
$ php artisan key:generate --ansi
```

进入宝塔运维主页，选择 [网站]，添加站点，域名为网站域名，修改网站目录的运行目录为 /public 



## 四. 管理权限问题

普通文件夹权限为 755 即可

storage，resources，scripts 权限必须至少 775

```shell
$ cd /www/wwwroot/120.48.100.162/getLCAI_web

$ chmod -R 775 storage/
$ chmod -R 775 resources/
$ chmod -R 775 scripts/
```



## 五. 优化项目部署

```shell
$ cd /www/wwwroot/120.48.100.162/getLCAI_web

$ php artisan config:cache # 生成配置缓存
$ php artisan route:cache # 生成路由缓存
$ npm run production # 运行 npm 产品环境
```

