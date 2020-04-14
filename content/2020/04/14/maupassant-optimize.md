---
title: "Maupassant 主题优化"
date: 2020-04-14T15:00:41+08:00
type: post
tags: ["hugo","maupassant","主题"]
categories: ["工具"]
toc: true
---

maupassant 是我最喜欢的一个主题，以下记录了对本博客主题的优化。

## 目录显示

在 `themes/maupassant/static/css` 目录下新建 `custom_style.css` 文件，填入以下内容，效果如左侧所示。

该版本可以自适应最长的标题，最宽为 300px = 放 17 个汉字

P.S. 请将鼠标移动到目录上测试

```css
.post-toc {
  overflow: hidden; /*隐藏溢出元素*/
  width: unset !important; /*清除原始宽度*/
  max-width: 50px; /*最初最大宽度*/
  transition: all 0.3s cubic-bezier(0.5, 1, 0.89, 1); /*过渡动画*/
}

.post-toc:hover,
.post-toc:active {
  max-width: 300px; /*展开最大宽度*/
  width: auto !important; /*自适应宽度*/
}
```

在 `config.toml` 中增加以下内容:

```toml
[params]
  customCSS = ['custom_style.css']
```

## 增加备案号

修改 `themes/maupassant/layouts/partials/footer.html`

```html
<footer id="footer">
  <div class="container">
    &copy; {{ now.Format "2006" }}
    <a href="{{ .Site.BaseURL | absURL }}"
      >{{ .Site.Title }} By {{ .Site.Author.name }}</a
    >.
    <!-- 修改开始---->
    <a href="http://www.beian.miit.gov.cn/" target="_blank"
      >豫ICP备18040132号-3</a
    >
    <!-- 修改结束---->
    Powered by
    <a
      rel="nofollow noreferer noopener"
      href="https://gohugo.io"
      target="_blank"
      >Hugo</a
    >. <a href="https://www.flysnow.org/" target="_blank">Theme</a> based on
    <a href="https://github.com/flysnow-org/maupassant-hugo" target="_blank"
      >maupassant</a
    >. {{ if .Site.Params.showHostPage }} Hosted by
    <a
      rel="nofollow noreferer noopener"
      href="https://pages.coding.me"
      target="_blank"
      >Coding Pages</a
    >. {{ end }}
  </div>
</footer>
```

## 去除 404 和 about 的 See Also

修改 `themes/maupassant/layouts/404.html`

```html
<div class="title404">
    <p>每一个平凡的日常<br />都是连续发生中的奇迹</p>
</div>
<!-- 删除开始---->
{{ partial "related" . }}
<!-- 删除结束---->
<a rel="nofollow" href="{{ .Site.BaseURL }}" class="index404">回首页看看</a>
```

修改 `themes/maupassant/layouts/_default/single.html`，只对类型为 post 和 tool 的启用

```
{{ if or (eq .Type "post") (eq .Type "tool") }}
  {{ partial "related" . }}
{{ end }}
```

## 修复列表对不齐

```css
.post-content ul li {
  text-indent: 0 !important;
}
```
