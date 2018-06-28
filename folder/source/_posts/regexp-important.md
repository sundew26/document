---
title: regexp-important
date: 2016/10/21 16:56
tags: javascript
---

## 正则表达式重点总结

![](https://mmbiz.qpic.cn/mmbiz_jpg/0vF1DtfHb3EIqLmAuHfMbLCr6Ad3C6Gw0KGt7ykePwac4YibOQzae5qjqIRmrgQXN0iaRpCOaSGk565SlfbWrSpw/0?wx_fmt=jpeg)

1\. 贪婪模式 （尽可能多的去匹配符合条件的字符串）

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /a.*b/ig; 
var newStr = str.replace(reg, '笨蛋'); 
console.log(newStr);
```

// 结果：笨蛋CCCCC  匹配了aaabbbbcccccAAABBBBCCCCC

**非贪婪模式（尽可能少的去匹配符合条件的字符串 '?' ）

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /a.*?b/ig; 
var newStr = str.replace(reg, '笨蛋'); 
console.log(newStr); 
```

// 结果：笨蛋bbbccccc笨蛋BBBCCCCC  匹配了aaabbbbcccccAAABBBBCCCCC

2\. 捕获组

**捕获型：

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
/[\w]{3}(b)*(c)*/.exec(str)
```

// 结果：\["aaabbbbccccc", "b", "c"\]  除了输出匹配结果，还输出了捕获到的b和c

**非捕获型3种：

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
/[\w]{3}(?!b)/.exec(str) 
```

// 结果：\["bbb"\]    后面跟的不是b的三个字符 aaabbbbcccccAAABBBBCCCCC

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
/[\w]{3}(?=b)/.exec(str) 
```

// 结果：\["aaa"\]    后面跟b的三个字符 aaabbbbcccccAAABBBBCCCCC

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
/[\w]{3}(?:b)/.exec(str)
```

// 结果：\["aaab"\]    三个字符后紧跟b的字符串 aaabbbbcccccAAABBBBCCCCC

**更好的理解捕获(分组) 

```javascript
var reg = /((\d)(\d))/; 
if(reg.test('abc123ddd')){ 
    console.log(RegExp.$0, RegExp.$1, RegExp.$2, RegExp.$3) 
} 
```

// 结果：undefined "12" "1" "2"     '(' 从左到右算分组，下标从1开始

3\. 方法：

test、match、search、replace、split、exec、compile

**test：测试str是否包含匹配，包含返回true，不包含返回false。

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /ab/ig; 
var newStr = reg.test(str); 
console.log(newStr); 
```

// 结果：true

**match：根据reg进行正则匹配，匹配到，返回匹配结果，否则返回null。

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /ab/ig; 
var newStr = str.match(reg); 
console.log(newStr); 
```

// 结果：\["ab", "AB"\]

**search ：根据reg进行正则匹配，如果匹配到一个结果，则返回它的索引数（0开始），否则返回-1。 

```javascript
ar str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /bc/ig; 
var newStr = str. search(reg); 
console.log(newStr); 
```

// 结果：6    下标从0开始

**replace：根据reg进行正则匹配，把匹配结果替换为“ 笨蛋 ”。

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /bc/ig; 
var newStr = str. replace(reg, '笨蛋'); 
console.log(newStr); 
```

// 结果：aaabbb笨蛋ccccAAABBB笨蛋CCCC

**split：根据reg进行正则分割，返回分割后的字符串组成的数组。

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /bc/ig; 
var newStr = str.split(reg); 
console.log(newStr); 
```

// 结果：\["aaabbb", "ccccAAABBB", "CCCC"\]    aaabbbbcccccAAABBBBCCCCC

**exec：对str进行正则处理，并返回匹配结果。array\[0\]为匹配到的字符串，array\[1\]为匹配在整个被搜索字符串中的位置。

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /bc/ig; 
var newStr = reg.exec(str); 
console.log(newStr);
```

// 结果：\["bc", index: 6, input: "aaabbbbcccccAAABBBBCCCCC"\]

**compile：用于改变和重新编译正则表达式(基本等同于构造方法方式，已被废弃)

```javascript
var str = "aaabbbbcccccAAABBBBCCCCC"; 
var reg = /bc/ig; 
var newStr = str.replace(reg, '笨蛋'); 
console.log(newStr); reg=/ab/gi; 
reg.compile(reg); 
newStr = str.replace(reg, '笨蛋'); 
console.log(newStr);
```

// 结果：aaabbb笨蛋ccccAAABBB笨蛋CCCC     aa笨蛋bbbcccccAA笨蛋BBBCCCCC   使用与否好像并没有区别，可以试试

##### [转自] [正则表达式重点总结](https://my.oschina.net/luweiweiwei/blog/761840)