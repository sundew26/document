---
title: hexo-css-weex-document
date: 2017/09/21
tags: blog
categories: 博客
---

# hexo+css项目部署到github #

#### 仿写weex使用手册 ####

## 一、概述
前面讲了如何使用hexo+css搭建自己的博客，今天主要是总结下如何把本地能访问的静态的博客部署到github上。以重写weex使用手册为例（不要问我为什么这么无聊，等你怀孕了就知道了）。

博客地址：https://stardew516.github.io/（迁移：https://stardew.github.io/）  
博客部署地址：  
https://github.com/stardew516/stardew516.github.io（https://github.com/stardew/stardew.github.io）

博客源码地址：https://github.com/stardew516/document
* 分支master: 原本打算用来部署，后面发现不可用，弃
* 分支development：基础代码存放，实现本地博客
* 分支deploy：修改一些信息，部署到github上所用

## 二、实现
##### 1. 使用hexo+css写好一套能在本地跑通的静态博客
* 可参照 [hexo+css创建自己的blog（搭建）](https://segmentfault.com/a/1190000011020260)

##### 2. 安装 hexo-deployer-git: `npm install hexo-deployer-git --save`

##### 3. 在github上新建一个仓库，注意命名格式如下图，用户名.github.io
![clipboard.png](https://segmentfault.com/img/bVVyqc)

##### 4. _config.yml 中配置
  ```
  # 部署部分的设置
  deploy:
    type: git
    repo: https://github.com/stardew516/stardew516.github.io.git
    branch: master
    message: hexo + css
  ```

##### 5. 生成文件: `hexo generate`

##### 6. 部署: `hexo deploy`

##### 7. 访问: https://stardew516.github.io/

##### [转自] [hexo+css项目部署到github（仿写weex使用手册）](https://segmentfault.com/a/1190000011294965)