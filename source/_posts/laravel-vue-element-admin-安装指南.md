---
title: laravel vue-element-admin 安装指南
date: 2022-10-22 13:20:26
tags: coding
---

[参考教程](http://www.phpxs.com/post/8290/)

# 环境

*php: ^7.4*

*laravel: 7.\**

*element: ^2.13.2*

*vue: ^2.6.10*

# 操作

##### 安装项目

更具体内容见 [此教程](https://squ1rrel-k.github.io/2022/10/14/Laravel-Vue-%E9%A1%B9%E7%9B%AE%E6%9C%AC%E5%9C%B0%E5%8C%96%E9%83%A8%E7%BD%B2/)

```shell
$ composer create-project laravel/laravel YourProjectName --prefer-dist "7.*"
```

##### 安装 vue-element-admin

```shell
$ git clone https://github.com/PanJiaChen/vue-element-admin.git
```

##### 合并 package.json

将 vue-element-admin 中 package.json 的 dependencies，devDependencies 

合并到 laravel 的 package.json 中

以 vue-element-admin 为主

##### 复制 babel.config.js 到 laravel 根目录

##### 复制项目

将 vue-element-admin 中整个 src 目录下的文件复制到 laravel 项目中的 resources/vue-element-admin 目录中

##### npm 安装

```shell
$ npm install
$ npm run dev
```

# 部分问题

##### 别名定义

```shell
Module not found: Error: Can't resolve '@/views/zip/index' in '/path/to/laravel-vue-admin/resources/backend/router'
```

在 webpack.mix.js 中增加项目 src 目录的别名

```js
// webpack.mix.js
mix.webpackConfig({
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'resources/vue-element-admin/src'),
    },
  },
})
```

##### babel 失败

```shell
Module build failed (from ./node_modules/babel-loader/lib/index.js):
```

复制 babel.config.js 到 laravel 根目录

##### 字体加载失败

```shell
 error  in ./resources/vue-element/src/assets/font/DS-DIGIT.TTF

Module parse failed: Unexpected character '' (1:0)
You may need an appropriate loader to handle this file type, currently no loaders are configured to process this file. See https://webpack.js.org/concepts#loaders
```

安装 npm 的 file-loader，ttf-loader

并在 webpack.mix.js 中增加关于新的 module loader 的 webpack config 

```shell
$ npm install file-loader ttf-loader -D
```

```javascript
//webpack.mix.js
mix.webpackConfig({
    resolve: {
        alias: {
            '@': path.resolve(__dirname, 'resources/vue-element/src'),
        },
    },
    
    //加入新的 module 的加载规则
    module: {
        rules: [
            {
                test: /\.TTF$/,
                use: [
                    {
                        loader: 'file-loader',
                        options: {
                            name: './font/[hash].[ext]',
                        },
                    },
                ]
            }
        ]
    }

})

```

##### 图片不显示

 ```html
src=[object module]
 ```

 vue 默认使用的是 commonjs，webpack ^4.* 使用的是 es6 语法，两边任意一边凑过去都可以

可以在 webpack.mix.js 的 rules 中加入以下（但是没有解决我的问题）

```javascript
{
  test: /\.(png|jpe?g|gif|svg)$/,
  loader: 'url-loader',
  options: {
    esModule: false
  }
}  	  
```

或可以降低 file-loader 的版本

 ```shell
$ npm install file-loader@3.*
 ```

##### 最后的 webpack.mix.js

```javascript
// webpack.mix.js
const mix = require('laravel-mix');

/*
 |--------------------------------------------------------------------------
 | Mix Asset Management
 |--------------------------------------------------------------------------
 |
 | Mix provides a clean, fluent API for defining some Webpack build steps
 | for your Laravel application. By default, we are compiling the Sass
 | file for the application as well as bundling up all the JS files.
 |
 */

mix.js('resources/vue-element/src/main.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css');

mix.webpackConfig({
    resolve: {
        alias: {
            '@': path.resolve(__dirname, 'resources/vue-element/src'),
        },
    },
    module: {
        rules: [
            {
                test: /\.TTF$/,
                use: [
                    {
                        loader: 'file-loader',
                        options: {
                            name: './font/[hash].[ext]',
                        },
                    },
                ]
            }
        ]
    }

})

```

