---
title: wechat
date: 2016/10/12 16:07
tags: front
---

## 微信小程序，试试水。

1\. https://mp.weixin.qq.com注册一个公众号，成为开发者，拿到一个appId。

2\. 下载微信开发者工具，https://mp.weixin.qq.com/debug/wxadoc/dev/devtools/download.html?t=1476197489869。

3\. 使用微信扫码登录

4\. 添加一个项目，把注册公众号获得到的appId复制到appId，名称目录填写好后，点击添加项目，显示

![](https://static.oschina.net/uploads/space/2016/1012/152416_w6pz_255575.png)

小程序还处于内测阶段，没有被邀请的用户获取的appId无法使用，尝试认证，但个人用户无法认证（有说关注大于500的可以，一时难以凑齐，弃之），因2013年以后公众号无法升级为服务号，于是又开始注册服务号，因为不是企业，没有各种相关信息，又弃之，最后只能选择无appId进行项目添加，虽少些功能，但也大体可以使用。

![](https://static.oschina.net/uploads/space/2016/1012/155359_Br3Z_255575.png)

往一个空的文件夹中添加项目，会自动创建一个获取信息和登录日志的小demo，结构非常清晰（加了几个接口和一个文件夹detail图）

.js => .js   .wxml => .html  .wxss => .css  .json => .json

![](https://static.oschina.net/uploads/space/2016/1012/155056_92hP_255575.png)

点击调试可以看到效果，头像，昵称，和helloword（因为是扫码登录，开发者工具绑定了开发者信息，所以可以拿到个人信息）。

![](https://static.oschina.net/uploads/space/2016/1012/155803_kszM_255575.png)

点击左侧编辑可对代码进行编辑，编辑完后保存、编译就可查看新效果。

![](https://static.oschina.net/uploads/space/2016/1012/160338_U0AQ_255575.png)

##### [转自] [微信小程序，试试水。](https://my.oschina.net/luweiweiwei/blog/757534)