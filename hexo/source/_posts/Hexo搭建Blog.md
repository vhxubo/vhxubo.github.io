---
title: Hexo搭建Blog
date: 2019-02-01 19:53:27
tags: 
excerpt: Hexo的基本操作，Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
photos:
---
> Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

## 所需环境
- [Node.js](https://nodejs.org/en/)
- [Git](https://git-scm.com/)

## 安装Hexo
Windows
```
$ npm install -g hexo-cli
```
## 常用命令行
[hexo官方文档](https://hexo.io/zh-cn/docs/)
```
$ hexo init <folder> //新建一个hexo项目
$ cd <folder>
$ npm install
```

```
$ hexo new [layout] <title> //新建一篇文章
```
layout: 可以在命令中指定文章的布局（layout），默认为 post，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局。

```
$ hexo server 
或
$ hexo s     //在本地部署预览
```

```
$ hexo generate //使用 Hexo 生成静态文件快速而且简单。
```

```
$ hexo clean && hexo deploy //清理后一键部署
`hexo d == hexo deploy`     
```

## 目录介绍
新建完成后，指定文件夹的目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
### _config.yml
网站的 配置 信息，您可以在此配置大部分的参数。

### package.json
应用程序的信息。EJS, Stylus 和 Markdown renderer 已默认安装，可以自由移除。

### scaffolds
模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。
Hexo的模板是指在新建的markdown文件中默认填充的内容。例如，如果您修改scaffold/post.md中的Front-matter内容，那么每次新建一篇文章时都会包含这个修改。

### source
资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

### themes
主题 文件夹。Hexo 会根据主题来生成静态页面。