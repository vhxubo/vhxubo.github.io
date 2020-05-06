---
title: 'xxy-web 踩坑记录'
date: 2020-04-20T13:12:16+08:00
type: post
tags: ['vue']
categories: ['记录', '开发者手册']
toc: true
---

`xxy-web` 将学小易 web 化，方便已注册用户搜题（需要先在学小易 APP 注册账号）。

[开源地址](https://github.com/vhxubo/xxy-web)

## 解决跨域问题

### dev 环境

在项目文件夹根目录新建 `vue.config.js` 文件，加入以下代码

```JavaScript
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'https://app.51xuexiaoyi.com',
        changOrigin: true,
      },
    },
  },
};
```

```
/api/v1/login -> https://app.51xuexiaoyi.com/api/v1/login
```

### 生产环境

修改 Nginx 配置文件,新增以下配置：

```conf
    location /api/
    {
        proxy_pass  https://app.51xuexiaoyi.com;
    }
```

这个地方遇到好几个坑，要修改指定网站下的配置文件、记得加分号。

## Nginx 路由 404

问题叙述：build 上传部署之后，在浏览器中直接打开 https://xxy.vhxubo.com/login 显示 404。

在 Nginx 配置文件中，新增一行 `try_files $uri $uri/ /index.html;`

```conf
server
{
    ......
    try_files $uri $uri/ /index.html;
    ......
}

```

具体部署请参见：[官方部署文档](https://cli.vuejs.org/zh/guide/deployment.html#docker-nginx)

## vue-router 页面跳转

```JavaScript
this.$router.push({ name: 'login' } // 跳转到 login 页面
this.$router.push({ path: '/' }) // 跳转到根路径
```

## 本地存储

```JavaScript
localStorage.setItem(key, value); // 存储数据
localStorage.getItem(key); // 读取数据
// 默认为 null
```

## 表单

```HTML
<form @submit.prevent="search" class="search-form">
  <div class="search__box">
    <input class="search__keyword" type="text" v-model="keyword" />
    <button class="search__submit" type="submit">查询</button>
  </div>
</form>
```
