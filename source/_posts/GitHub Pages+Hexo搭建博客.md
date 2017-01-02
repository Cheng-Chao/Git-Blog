title: GitHub Pages+Hexo搭建博客
date: 2017/1/2 20:20
categories:
- GitHub
- Hexo
tags:
- 博客
- GitHub Pages
- Hexo
---
Hexo 是一个简单地、轻量地、基于Node的一个静态博客框架，可以方便的生成静态网页托管在Github和Heroku上；GitHub Pages 可以被认为是用户编写的、托管在github上的静态网页。由于它的空间免费稳定，可以用于介绍托管在Github上的Project或者搭建网站。本文为一个简易的教程。
<!--more-->

----
## 前置条件
### 安装Node
**Hexo**是基于**Node**的，所以首先的安装Node.js，去官网去下载一个安装包就好[Node.js](https://nodejs.org/en/)。如果你还没有安装过**Git**，推荐你安装一个[Git](https://msysgit.github.io)。安装好之后打开**Git Bash**，使用以下命令就可以查看**Node**是否装好。
```shell
$ node -v
v6.9.2
```
**Node**的一个提高效率的工具就是**npm**，全称是**Node Package Manager**  ，是一个**Node.js**包管理和分发工具，已经成为了非官方的发布Node模块（包）的标准。如果你熟悉Ruby的gem，Python的pypi、setuptools，PHP的pear，那么你就知道NPM的作用是什么了。**Git Bash**，使用以下命令就可以查看**npm**的版本。在刚刚安装**node**的时候，**npm**已经装好了。
```shell
$ npm -v
3.10.9
```
接下了你就可以使用**npm install**来安装基于**node**的第三方包了，和**\*nix**系统的命令行工具类似。但是由于国内的网络环境，建议将**node**的安装源设为阿里的同步镜像源。
```shell
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```
然后就可以使用**cnpm install [name]**来安装模块了，速度快很多。
### 安装Hexo
配置好**Node.JS**后，打开**Git Bash**的命令工具输入以下命令:
```shell
cnpm install hexo-cli -g
cnpm install hexo --save
```

----
## 配置本地Hexo博客
### 初始化本地目录
随便新建个文件夹列如（D:\hexo-demo），使用**Git Bash**的命令工具进入该路径下，执行以下命令:
```shell
hexo init

#新建完成后，指定文件夹的目录如下
.
├── _config.yml
├── package.json
├── scaffolds
├── scripts
├── source
|      └──posts
└── themes
```
### 安装Hexo插件
在本地博客根目录下使用**Git Bash**的命令工具执行以下命令:
```snpm install hexo-generator-index --save
cnpm install hexo-generator-archive --save
cnpm install hexo-generator-category --save
cnpm install hexo-generator-tag --save
cnpm install hexo-server --save
cnpm install hexo-deployer-git --save
cnpm install hexo-deployer-heroku --save
cnpm install hexo-deployer-rsync --save
cnpm install hexo-deployer-openshift --save
cnpm install hexo-renderer-marked@0.2 --save
cnpm install hexo-renderer-stylus@0.2 --save
cnpm install hexo-generator-feed@1 --save
cnpm install hexo-generator-sitemap@1 --save
```
### 本地配置
初始的时候可以见到配置下。
```yml
# Hexo Configuration
## Docs: http://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/
# Site 站点配置
title: Hexo-demo #网站标题
subtitle: hexo is simple and easy to study #网站副标题
description: this is hexo-demo #网栈描述
author: pomy #你的名字
language: zh-CN #网站使用的语言
timezone: Asia/Shanghai #网站时区
# URL #可以不用配置
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yoursite.com #网址，搜索时会在搜索引擎中显示
root: / #网站根目录
permalink: :year/:month/:day/:title/ #永久链接格式
permalink_defaults: #永久链接中各部分的默认值
# Directory 目录配置
source_dir: source #资源文件夹，这个文件夹用来存放内容
public_dir: public #公共文件夹，这个文件夹用于存放生成的站点文件
tag_dir: tags #标签文件夹
archive_dir: archives #归档文件夹
category_dir: categories #分类文件夹
code_dir: downloads/code #Include code 文件夹
i18n_dir: :lang #国际化文件夹
skip_render: #跳过指定文件的渲染，您可使用 glob 来配置路径
# Writing 写作配置
new_post_name: :title.md # 新文章的文件名称
default_layout: post #默认布局
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0 #把文件名称转换为 (1) 小写或 (2) 大写
render_drafts: false #显示草稿
post_asset_folder: false #是否启动资源文件夹
relative_link: false #把链接改为与根目录的相对位址
future: true
highlight: #代码块的设置
enable: true
line_number: true
auto_detect: true
tab_replace:
# Category & Tag 分类 & 标签
default_category: uncategorized #默认分类
category_map: #分类别名
tag_map: #标签别名
# Date / Time format 时间和日期
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss
# Pagination 分页
## Set per_page to 0 to disable pagination
per_page: 10 #每页显示的文章量 (0 = 关闭分页功能)
pagination_dir: page #分页目录
# Extensions 扩展
## Plugins: http://hexo.io/plugins/ 插件
## Themes: http://hexo.io/themes/ 主题
theme: landscape #当前主题名称
# Deployment #部署到github
## Docs: http://hexo.io/docs/deployment.html
deploy:
type:
```
### 本地查看效果
继续执行以下命令，成功后可在浏览器输入localhost:4000查看效果。
```shell
hexo server
//the same as
hexo s
```
如果配置成功，即可在浏览器中看到**hexo**初始默认的**hello world**博文。

----
## 部署到GitHub
### 新建repo
在GitHub新建一个repo，名字为**github-user-name.github.io**，这是**GitHub Pages**的默认域名。然后使用**git clone**将repo下到本地。
### 静态文件
在本地博客根目录下使用**Git Bash**的命令工具执行以下命令:
```shell
hexo generate
//the same as
hexo g
```
然后会在根目录下生成一个**public**文件夹，里面为博客对应的静态网页文件。将**public**文件夹下的所有文件/文件夹拷到刚刚新建repo的本地目录下，然后将所有内容**publish**到**GitHub**。然后就可以使用**https://github-user-name.github.io**就可以访问博客了，到这里博客就搭建完成了。

----
## 博客优化
### 主题
**hexo**博客有很多主题，如果喜欢折腾，可以将博客整得很好看，这里推荐使用**NexT**，也是我正在用的主题。其**GitHub**主页上面有很详细的说明。  
[hexo](https://github.com/hexojs/hexo)
[使用文档](http://theme-next.iissnan.com/getting-started.html)        
