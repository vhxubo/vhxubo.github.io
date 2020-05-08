---
title: "LitNews 踩坑记录"
date: 2020-05-08T18:41:11+08:00
type: post
tags: ["vue", "electron-vue", "electron"]
categories: ["记录"]
toc: true
---

## GitHub Actions 编译

使用 GitHub Actions 进行多端编译

### MacOS 错误提示

```
Can't locate Mac/Memory.pm in @INC (you may need to install the Mac:: Memory module)
```

**解决方案：**

```bash
npm install electron-builder@latest -D
```

### Windows 编译出错

需要为 Windows 配置基础环境,windows-build-tools 出现

```
------------------- Python --------------------
Successfully installed Python 2.7---------- Visual Studio Build Tools ----------
Still waiting for installer log file...
```

**解决方案：**

```bash
npm install --global --production windows-build-tools@4.0.0
```
