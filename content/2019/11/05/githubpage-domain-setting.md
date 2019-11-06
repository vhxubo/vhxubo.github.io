---
title: "Hugo + GithubPage 自定义域名并支持 HTTPS"
date: 2019-11-05T21:16:48+08:00
type: post
tags: ["GithubPage","Domain","Hugo"]
categories:
  - "开发者手册"
toc: true
---
## 未完待补充
> 忽然觉得 WordPress 的 maupassant 主题没有 Hugo 上的好看，而且基本不用 WordPress，以及学生机访问较慢，还是直接设置 blog.zxbzn.com 指向 anguoi.github.io 好了。

域名提供商：阿里云

本文基于 Wercker 自动部署 Hugo 到 GithubPage 的设置

## 阿里云域名解析
使用 cmd 执行命令行，获得 ip 地址
```
ping xxxx.github.io 
(xxxx 为你的 GitHub 账户名)
```

如下，可获得 ip 为 `185.199.108.153`
![cmdping.png](cmd.png)

打开阿里云域名解析设置，新增主机记录

记录类型: A

主机记录为你的自定义域名

记录值为上面获得的 ip 
![aliyun.png](aliyun.png)

## Custom domain 设置
直接将自定义域名添加到 `Custom domain` 里面 `Save`

点击 `Enforce HTTPS` 单选框支持 HTTPS

## Hugo 配置
`config.toml` 

```toml
# 注意换成你的自定义域名
baseURL = "https://blog.zxbzn.com/"
```

`wercker.yml`

```yml
# 注意换成你的自定义域名
- nztomas/gh-pages@0.2.4:
    domain: blog.zxbzn.com
```