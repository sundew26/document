---
title: mCustomScrollbar-config
date: 2015/01/19 15:54
tags: components
categories: 组件
---

## mCustomScrollbar常用配置

mCustomScrollbar是一个非常好用的滚动条插件，一般情况下只需作如下配置即可。  

```
require(['jquery','mCustomScrollbar'],function($,mCustomScrollbar){
    $(".submenu-content").mCustomScrollbar({
        autoHideScrollbar: true,
        horizontalScroll:false
    });
});
```
 <!-- more -->
```
.mCSB_scrollTools .mCSB_draggerRail{background-color: #c6c4c2;width: 8px;}

.mCSB_scrollTools .mCSB_dragger .mCSB_dragger_bar{background-color: #c6c4c2;}

.mCSB_scrollTools .mCSB_dragger:hover .mCSB_dragger_bar,.mCSB_scrollTools .mCSB_dragger:active .mCSB_dragger_bar,.mCSB_scrollTools .mCSB_dragger.mCSB_dragger_onDrag .mCSB_dragger_bar {background-color: #938B89;}

.ui-state-default{background:none;}

.accordion-hov,.accordion-click{background-color:#6e8fd0;color:#ffc600;}

.copyright{line-height:30px;background-color:#a3a3a3;}

.mCSB_scrollTools.mCSB_scrollTools_horizontal .mCSB_draggerRail {height: 8px;margin: 4px 0;}
```

##### [转自] [mCustomScrollbar常用配置](https://my.oschina.net/luweiweiwei/blog/369341)