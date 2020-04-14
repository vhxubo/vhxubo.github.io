---
title: "优化网页加载速度"
date: 2020-04-14T19:42:53+08:00
type: post
tags: ["Hugo"]
categories: ["记录"]
toc: true
---

## PageSpeed Insights

在线分析网页加载: https://developers.google.com/speed/pagespeed/insights/

## 优化 CSS 加载速度

CSS 加载的速度取决于加载总时长与总体积，
我们分两步进行优化：

1. 合并 CSS 文件，以减少加载总时长；
2. 压缩 CSS 文件，以减少体积。

### 合并 CSS 文件

全局安装 [concat](https://www.npmjs.com/package/concat)

```bash
npm i concat -g
```

将 `custom_style.css`,`normalize.css`,`oldstyle.css`(原 style.css) 合并为 `style.css`

```bash
concat -o style.css ./custom_style.css ./normalize.css ./oldstyle.css
```

这样就将已有的三个访问请求转换为了一个请求。

### 压缩 CSS 文件

全局安装 [minify](https://www.npmjs.com/package/minify)

```bash
npm i minify -g
```

压缩 `style.css`，生成 `style.min.css`

```bash
minify style.css
```

### 修改 CSS 引用

找到主题中对 CSS 引用部分，注释或者删除，添加对 `style.min.css` 的引用即可。

## 执行 Hugo 自带的压缩命令

```bash
hugo --minify
```
