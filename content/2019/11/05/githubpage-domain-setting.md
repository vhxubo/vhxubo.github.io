---
title: "Hugo + GithubPage 自定义域名并支持 HTTPS"
date: 2019-11-05T21:16:48+08:00
lastmod: 2019-11-06T23:17:40+08:00
type: post
tags: ["GithubPage","Custom domain","Hugo"]
categories:
  - "开发者手册"
toc: true
---
因为 WordPress 的 maupassant 主题没有 Hugo 上的好看，而且基本不用 WordPress，以及学生机访问较慢，所以决定将 blog.vhxubo.com 设置为 vhxubo.github.io 的 Custom domain，白嫖 Github。

根据网上已有文章，新增 A 记录设置 Custom domain 后，发现 GithubPage 有如下提示:

> Your site's DNS settings are using a custom subdomain, blog.vhxubo.com, that's set up as an A record. We recommend you change this to a CNAME record pointing at [YOUR USERNAME].github.io. For more information, see https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/.

大概意思是: 不推荐使用`A 记录 - 将域名指向一个 IPV4 地址`，应该更换为`CNAME - 将域名指向另一个域名`，记录值填写为: [YOUR USERNAME].github.io。

所以，为啥呢？

以我的 vhxubo.github.io 为例，每隔段时间后执行`ping vhxubo.github.io`，对应的 IP 值会有所改变。

可以得出：设置 A 记录，只能指向某个 IP；而设置 CNAME 记录，则可以跳转到多个 IP。

---

域名提供商：阿里云。

本文基于`Wercker 自动部署 Hugo 到 GithubPage`的设置（博文待发布）。

## 新增 CNAME 记录 
打开阿里云域名解析设置，新增主机记录：

- 记录类型: CNAME - 将域名指向另外一个域名
- 主机记录: blog
- 记录值: [YOUR USERNAME].github.io
  
主机记录与记录值必须与你自己的对应，否则不能生效，我的设置如下图所示。

![aliyun-setting](aliyun-setting.png)

## Custom domain 设置
将自定义域名输入`Custom domain`里面，点击`Save`。

单选框`Enforce HTTPS`打勾，以支持 HTTPS，如下图所示。

![githubpage-setting](githubpage-setting.png)

## Hugo 配置
`config.toml` 

```toml
# 注意换成你的自定义域名
baseURL = "https://blog.vhxubo.com/"
```

`wercker.yml`

```yml
# 注意换成你的自定义域名
- nztomas/gh-pages@0.2.4:
    domain: blog.vhxubo.com
```
