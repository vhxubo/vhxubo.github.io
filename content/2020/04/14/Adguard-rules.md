---
title: "Adguard Rules"
date: 2020-04-14T11:05:06+08:00
type: post
tags: ["Adguard"]
categories: ["工具"]
toc: true
---

## 知乎

每当我打开知乎，刷新推荐，第一个必然是视频，然后我就得沉迷其中，忘却我打开知乎的真正目的。

这严重影响了我的日常进度，知乎啊！我就是打开你找点资料呀！！

那就让我干掉你推荐的视频吧，嘻嘻嘻。

### 去除知乎推荐的视频

```
||api.zhihu.com/topstory/recommend*$replace=/{"id".+?"video".+?null}\,?//s
```

### 将推荐大图改为小图

```
||api.zhihu.com/topstory/recommend*$replace=/"BIG_IMAGE"/"SMALL_IMAGE"/s
```

### 不显示视频，只显示文字

```
||api.zhihu.com/topstory/recommend*$replace=/"video"/"novideo"/s
```

## 哔哩哔哩

与知乎相反，我只想让哔哩哔哩安安静静的做一个视频软件。

### 去除哔哩哔哩推荐的文章/动态

```
||app.biliapi.com/x/v2/feed/index$replace=/{"card_type":"one_pic_v3".+?}\,{"card_type"/{"card_type"/s
||app.bilibili.com/x/v2/feed/index$replace=/{"card_type":"one_pic_v3".+?}\,{"card_type"/{"card_type"/s
```
