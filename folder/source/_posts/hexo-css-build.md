---
title: hexo-css-build
date: 2017/09/05
tags: blog
categories: 博客
---

# hexo+css创建自己的blog（搭建） #

## 一、什么是hexo
Hexo是一个快速、简洁且高效的博客框架，使用Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。目前比较火的vue和weex的文档都是使用hexo框架实现的。
 <!-- more -->
## 二、hexo的安装
安装hexo前，确保电脑中已经安装了node和git。
### node安装
```
方法一、
    直接安装node：ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
方法二、
    先安装homebrew： /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    后安装node：brew install node
```

### git安装
```
先安装homebrew： /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
后安装git：brew install git
```

### hexo安装
```
npm install -g hexo-cli
```

## 三、创建项目
1. 新建项目: `hexo init folder`
2. 进入: `cd folder>`
3. 安装依赖包: `npm install`
4. 新建一篇文章: `hexo new iOS-APIs` (文件会在/source/_posts下)
5. 启动: `hexo server`
6. 浏览器打开: `http://localhost:4000/document/`

## 四、hexo配置
配置文件为_config.yml
参考: https://hexo.io/docs/configuration.html
github: https://github.com/hexojs/hexo/

### Site （网站）
1. 网站标题
title: weex使用手册
2. 网站副标题
subtitle: weex中文手册
3. 网站描述
description: 整理weex手册, 包括通用特性, 内建组件, 内建模块, CSS 单位, 通用事件, Native DOM APIs, Weex 实例变量, Web 标准, JS Service, Vue, 高阶知识, 迁移
4. 作者名字
author: stardew
5. 网站使用的语言
language: 简体中文
6. 网站时区Hexo 默认使用您电脑的时区。时区列表。比如说：America/New_York, Japan, 和 UTC 。
timezone: UTC

### URL （网址）
如果您的网站存放在子目录中，例如 http://yoursite.com/blog，则请将您的 url 设为 http://yoursite.com/blog 并把 root 设为 /blog/。
1. 网址
url: https://github.com/stardew516/document
2. 网站根目录
root: /document/
3. 文章的 永久链接 格式
permalink: :year/:month/:day/:title/
4. 永久链接中各部分的默认值
permalink_defaults:

### Directory （目录）
1. 资源文件夹，这个文件夹用来存放内容。
source_dir: source
2. 公共文件夹，这个文件夹用于存放生成的站点文件。
public_dir: public
3. 标签文件夹
tag_dir: tags
4. 归档文件夹
archive_dir: archives
5. 分类文件夹
category_dir: categories
6. Include code 文件夹
code_dir: downloads/code
7. 国际化（i18n）文件夹
i18n_dir: :lang
8. 跳过指定文件的渲染，您可使用 glob 表达式来匹配路径。
skip_render:

### Writing （文章）
1. 新建文章的文件名称
new_post_name: :title.md
2. 预设布局
default_layout: post
3. 在中文和英文之间加入空格
auto_spacing: false
4. 把标题转换为 title case
titlecase: false
5. 在新标签中打开链接
external_link: true
6. 把文件名称转换为 (1) 小写或 (2) 大写
filename_case: 0
7. 显示草稿
render_drafts: false
8. 启动 Asset 文件夹
post_asset_folder: true
9. 把链接改为与根目录的相对位址
relative_link: false
10. 显示未来的文章
future: true
11. 代码块的设置
    highlight:
      enable: true
      line_number: true
      auto_detect: true
      tab_replace:
  
### Home page setting （主页设置）
    1. path: 博客索引页的跟路径,默认为空
    2. per_page: 每页展示的文章量, 为0时表示不分页
    3. order_by: 排序, 默认日期降序
    index_generator:
      path: ''
      per_page: 10
      order_by: -date
  
### Category & Tag （分类 & 标签）
1. 默认分类
default_category: uncategorized
2. 分类别名
category_map:
3. 标签别名
tag_map:

### Date / Time format （日期 / 时间格式）
hexo使用Moment.js来解析和显示时间。
可以参照http://momentjs.com/docs/#/displaying/format/来自定义日期格式。
1. 日期格式
date_format: YYYY-MM-DD
2. 时间格式
time_format: HH:mm:ss

### Pagination （分页）
1. 每页显示的文章量 (0 = 关闭分页功能)
per_page: 10
2. 分页目录
pagination_dir: page

### Extensions （扩展）
插件: https://hexo.io/plugins/
主题: https://hexo.io/themes/
1. 当前主题名称。值为false时禁用主题
theme: landscape

### Deployment （部署）
参考: https://hexo.io/docs/deployment.html
2. 部署部分的配置
    deploy:
      type: git
      repo: https://github.com/stardew516/document
      branch: master
      message: hexo + css

## 五、部署
github上部署:
1. 安装hexo-deployer-git: `npm install hexo-deployer-git --save`
2. _config.yml 中配置
  ```
  # 部署部分的设置
  deploy:
    type: git
    repo: https://github.com/stardew516/document
    branch: master
    message: hexo + css
  ```
3. 终端进入目录,运行: `hexo deploy`

##### [转自] [hexo+css创建自己的blog（搭建）](https://segmentfault.com/a/1190000011020260)