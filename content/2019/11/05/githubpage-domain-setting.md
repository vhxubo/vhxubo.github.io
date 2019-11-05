---
title: "Hugo + GithubPage 自定义域名并支持 HTTPS"
date: 2019-11-05T21:16:48+08:00
type: post
tags: ["GithubPage","Domain"]
categories:
  - "笔记"
toc: true
---
## 未完待补充
> 忽然觉得 WordPress 的 maupassant 主题没有 Hugo 上的好看，而且基本不用 WordPress，以及学生机访问较慢，还是直接设置 blog.zxbzn.com 指向 anguoi.github.io 好了。

域名提供商：阿里云

本文基于 Wercker 自动部署 Hugo 到 GithubPage 的设置

## 阿里云域名解析
使用 cmd 执行命令行 ping xxxx.github.io (xxxx 为你的 GitHub 账户名)获得 ip 地址

如下，可获得 ip 为 185.199.110.153
```
$ ping anguoi.github.io
正在 Ping anguoi.github.io [185.199.110.153] 具有 32 字节的数据:
来自 185.199.110.153 的回复: 字节=32 时间=118ms TTL=53
来自 185.199.110.153 的回复: 字节=32 时间=114ms TTL=53
来自 185.199.110.153 的回复: 字节=32 时间=113ms TTL=53
来自 185.199.110.153 的回复: 字节=32 时间=116ms TTL=53

185.199.110.153 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
往返行程的估计时间(以毫秒为单位):
    最短 = 113ms，最长 = 118ms，平均 = 115ms
```

打开阿里云域名解析设置，新增主机记录，记录类型 A，主机记录为你的自定义域名，记录值为上面获得的 ip 

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