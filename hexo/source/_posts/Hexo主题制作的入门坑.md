---
title: Hexo主题制作的入门坑
date: 2019-02-02 18:03:09
tags:
excerpt: Hexo主题制作的入门坑
photos:
---
>该文档包含所需项目的简介与基础用法，略有赘余，可以直接看`Tips`
## Hexo Theme Unit Test
>This is a dummy Hexo site for theme unit test. You should test your theme before release.
>This test doesn't contain the default theme. You have to install the theme you want to test before starting.

[GitHub](https://github.com/hexojs/hexo-theme-unit-test)
### Usage
- Clone this repository
```
$ git clone https://github.com/hexojs/hexo-theme-unit-test.git
```
- Install your own theme and modify theme setting in _config.yml.

- Run server and start testing. Make sure all styles are displayed properly.

- Once test is done, you can submit your theme!

### Tips
- 记得输入命令行，安装所需的库
```
npm install
```
- 需要在根目录下新建一个`themes`文件夹，用来存放主题文件夹

- 如果想将该项目文件夹，上传到自己的Github库中，记得将该文件夹中的`.git`文件夹删除

## generator-hexo-theme
>Generate a hexo theme

[GitHub](https://github.com/tcrowe/generator-hexo-theme)

### Install
```
$ npm install --global yo
$ npm install --global generator-hexo-theme
```
### Use
If you don't have a site yet create one with hexo init hexo-cli.
```
$ mkdir my-site
$ cd my-site
$ hexo init
```
Navigate to the directory you want to place the theme project in (most likely themes/).
```
# from the site root
$ cd themes

# make a new theme directory
$ mkdir my-theme
$ cd my-theme

# generate
yo hexo-theme
```
1. Check _config.yml in your main blog directory
- Set theme property to your theme name, activating this theme
2. Check _config.yml in your theme directory
- Change menu items if needed
- Change stylesheet and scripts list if needed
3. Navigate back to your main blog directory
4. `hexo server --debug`