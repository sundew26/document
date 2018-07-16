---
title: isarray
date: 2017/02/17
tags: javascript
categories: 前端基础
---

# 鉴别数组 #
![](https://mmbiz.qpic.cn/mmbiz_jpg/0vF1DtfHb3F22ruqIzJNWgnugCYFB4eOy83XFBiaS39FuXujVjpvicCMA1gNE3IIrInwmpExmfnRg0vcEVWwEHSg/0?wx_fmt=jpeg)

判断一个对象是否是数组，有五种方法，如下：  
 <!-- more -->
```
var arr = [1, 2, 3];
var obj = {a:1};

toString返回对象的字符串表示
toString.apply(arr) === '[object Array]';  // true
toString.apply(obj) === '[object Array]'; // false

Object.prototype.toString.call(arr) === '[object Array]'; // true
Object.prototype.toString.call(obj) === '[object Array]'; // false

arr instanceof Array; // true
obj instanceof Array; // false

Array.isArray(arr); // true
Array.isArray(obj); // false

// constructor 指向创建当前对象的构造函数
arr.constructor === Array // true
obj.constructor === Array // false
```

PS：  
基本数据类型只有五种：Null, Undifined, String, Number, Boolean  
引用类型：Array，Object，Function  

##### [转自] [鉴别数组](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483777&idx=1&sn=afaa43f8aeda14494fc1f0548bea5f4a&chksm=eb02a1f7dc7528e1ad1de8480cc960950aaf4fb48481a707c2b4049e8cf38a4f9869671abdd5&mpshare=1&scene=1&srcid=0628bOSEN5a1yDfO54Rz1qKb&key=d8aade18608a3d7081d281c4945d2a5ae2411e3cdb859bc5aef4f6045ad3c7c0b8f450da58d17806dda7df259b7ee472994a556c047ce7c8259165fbda1baf5614aa0777c33d4c2fb4ee1835056faa60&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)