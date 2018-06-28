---
title: javascript-advantages-disadvantages
date: 2016/12/06
tags: javascript
categories: 前端基础
---

![](https://mmbiz.qpic.cn/mmbiz_jpg/0vF1DtfHb3E7oG0qEetwfwjeeSAEPKIpTDjXAEGwbhAQrP9MY9eXawxmbibTvvfkE0abiacTiafjR1TZYY6OEr0qQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5)

参考javascript语言精粹附录及网友总结  

#### 优点：简单、灵活、跨平台  

1. 非常简单
* a. 单线程  

2. 灵活
* a. 灵活是指代码要实现某个功能时，可以写的很简单，也可以很复杂  
* b. 可以函数式编程（闭包）函数是顶级对象，函数是有词法作用域的闭包  
* c. 也可以面向对象编程，基于原型继承的动态对象  
* d. 字面量，对象字面量和数组字面量（json灵感之源）  

3. 跨平台

* a. 跨系统平台以及浏览器平台,有不兼容问题  

#### 缺点：全局变量有隐患、无块级作用域、隐式类型转换错乱、闭包隐患、typeof判断不全面、+功能不明确  

1. 全局变量（最糟糕的设计）：
* a. 大程序里难以管理，因为全局变量可以被程序的任何部分在任意时间修改，使得程序行为变得极度复杂。降低了程序的可靠性。  
* b. 独立子程序变得复杂，因为如果子程序存在和全局变量名相同的变量时，会导致冲突，不容易调试。  
* c. 未声明的变量默认为全局变量，bug难找。  
2. 没有自带的块级作用域（ES6改善）
3. 自动插入分号，有时会不合时宜的插入分号，掩盖严重错误。
4. 有很多保留字很少使用，byte，enum，implements，native，package，short，volatile
5. typeof判断不全面
* typeof null  
* typeof array  
6. parseInt，遇到非数字会停止解析
7. +可能是数字相加、也可能是字符串连接
8. 浮点数0.1+0.2 != 0.3
9. NAN  NAN != NAN
10. 伪数组，javascript没有真正的数组
```
var arr = [1,2];
if (arr && typeof arr === 'object' && arr.constructor === Array) {
  console.log('true');
}
```
11. 假值
12. 设计比较仓促（只花了10天）
13. 没有继承

##### [转自] [javascript优缺点](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483670&idx=1&sn=e6b500200169af4651b5d189b60c3c36&chksm=eb02a160dc7528763a5bf2d66f80bd8fab5cac54a049e650254d09e657b5a660312fde0ecd67&mpshare=1&scene=1&srcid=0628YJlNOUEIHg4xRG5ZrqYj&key=cf0dc319bc22985e0492734baa44d3acf506f37e0e349998e38237bab75cec966f6288b87acb4d89cb65488bc6b9ab66e8ee7f58ea0ca80472335fd06823cf66dee87b1146b806506cff35cf9f39e373&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)