---
title: regexp-password
date: 2017/04/06 11:35
tags: javascript
categories: 前端基础
---

## 正则校验密码规则

1\. 8-16位数字、字母和特殊字符~!@#$%^&*-+=_.
```
var reg = /^\[~!@#$%^&*\\-+=_.0-9a-zA-Z\]{8,16}$/;  
var str = '1wfwe@99$;' // 有分号  
console.log(reg.test(str))
```
 <!-- more -->
2\. 8-16位，且必须只包含数字、字母和特殊字符~!@#$%^&*-+=_.
```
var reg = /^(?=\[~!@#$%^&*\\-+=_.0-9a-zA-Z\]*\[~!@#$%^&*\\-+=_.\])(?=\[~!@#$%^&*\\-+=_.0-9a-zA-Z\]*\[0-9\])(?=\[~!@#$%^&*\\-+=_.0-9a-zA-Z\]*\[a-zA-Z\])\[~!@#$%^&*\\-+=_.0-9a-zA-Z\]{8,16}$/;
var str = '1w@2812fhif94#$%1'    // 17位
console.log(reg.test(str))
```

3\. 感觉上面的有点长，replace了一下，但是看着也没多好，将就下吧。
```
注：
x = '~!@#$%^&*\\\-+=_.'  // 特殊字符
d = '0-9'  // 数字
w = 'a-zA-Z' // 字母

var reg = '^(?=\[xdw\]*\[x\])(?=\[xdw\]*\[d\])(?=\[xdw\]*\[w\])\[xdw\]{8,16}$'.replace(/x/gi, '~!@#$%^&*\\\-+=_.').replace(/d/gi, '0-9').replace(/w/gi, 'a-zA-Z');
reg = new RegExp(reg);
var str = '1w@28194#$%<' // 有<
console.log(reg, reg.test(str))
```

注：特殊字符里的‘-’需要转义‘\\-’, 3中需要‘\\\-’

##### [转自] [正则校验密码规则](https://my.oschina.net/luweiweiwei/blog/873937)