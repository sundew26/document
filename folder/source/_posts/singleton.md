---
title: singleton
date: 2016/12/7
tags: javascript
categories: 前端基础
---

# 单例模式（创建型） #

定义：一个类仅有一个实例，并提供一个访问它的全局访问点。  

原理：使用一个变量来标志当前是否已经为某个类创建过实例对象，如果没有，就创建一个类实例对象，并把值赋给存储实例的变量。如果有，则在下一次获取该类的实例时，直接返回之前创建的实例对象。  
 <!-- more -->
![](https://mmbiz.qpic.cn/mmbiz_png/0vF1DtfHb3EwLUfibiadGz4P373eRQCyErTrN0t8OfNsZnsfjHmFJJic2eQt4ucbnhTicRTocMk2mr7zC5fPdJrv5Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1)

举例：用一个经典的弹窗功能来举例，下面是单例模式的形成  

##### 1.点击按钮出现弹窗（多次点击，出现多个浮层）  
```
var createMask = function () {

  return document.body.appendChild(document.createElement('div'));

}

$('button').click(function () {

  var mask = createMask();

});
```

##### 2.添加一个全局标识，如果有直接返回，没有的话则创建（全局变量容易被污染）  
```
var mask;

var createMask = function () {

  if (mask) {

    return mask;

  } else {

    mask = document.body.appendChild(document.createElement('div'));

    return mask;

  }

}
```

##### 3.使用闭包，保护变量（适用性不广）  
```
var createMask = function () {

  var mask;

  return function () {

    return mask || (mask = document.body.appendChild(document.createElement('div')));

  }

}();
```

##### 4.单例模式（封装一个单例）·  
```
var singleton = function (fn) {

  var result;

  return function () {

    return result || (result = fn.apply(this, arguments));

  }

}

var createMask = singleton(function () {

  return document.body.appendChild(document.createElement('div'));

});
```

##### [转自] [单例模式（创建型）](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483672&idx=1&sn=a822fbd05849d6a8e3d20f6f375f75d5&chksm=eb02a16edc752878389816993313491fa62e7e0271a283a232040170774a68461469e8e801ef&scene=0&key=ef4707cb1c7d18b4e5e2a5765dd943b6ec10570d1b5a4bac3e4ebc38b2208e232dd17bd09cee2f65f364d8c7d2158792d61759754ae4ca46c47c72b1d68a86a777b7a454e3f77fa3442856a4c18ca988&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)