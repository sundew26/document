---
title: this
date: 2017/02/10
tags: javascript
categories: 前端基础
---

![](https://mmbiz.qpic.cn/mmbiz_jpg/0vF1DtfHb3FiaxWvAb4GHrpmBlIphvVkCnqBAm6o9AYoVRKPddk6L4OdlLQcxKUheTgR7QpvcIloHAKFiahA4CsQ/0?wx_fmt=jpeg)

判断 this 指向谁，看执行时而非定义时，只要function没有绑定在对象上调用，它的 this 就是window。  
箭头函数的特征是，定义在哪，this 就指向哪。  

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <!--允许全屏-->
  <meta content="yes" name="apple-mobile-web-app-capable" />
  <meta content="yes" name="apple-touch-fullscreen" />
  <meta name="data-spm" content="a215s" />
  <meta content="telephone=no,email=no" name="format-detection" />
  <meta content="fullscreen=yes,preventMove=no" name="ML-Config" />
  <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no"/>
  <title>this</title>
</head>

<body>
  <div id="dom" onclick="getId()">this:</div>
  <p>this关键字总是返回一个对象</p>
  <p>this总是指向类的当前实例</p>
  <p>this 不能赋值</p>
  <p>this 不能脱离 类/对象<p>
  <p>this 是面向对象语言里常见的一个关键字</p>
  <p>判断 this 指向谁，看执行时而非定义时，只要函数(function)没有绑定在对象上调用，它的 this 就是 window。</p>  
  <p>箭头函数的特征就是，定义在哪，this 就指向哪。</p>
  
  <script>
   // "use strict";

   // this和构造函数
    function Company() {
      this.name = 'stardew';
      console.log(this, typeof this); // Company "object"
    }
    var company = new Company();
    console.log(company.name);  // stardew

    // this和对象
    var company = {
      name: 'stardew',
      member: 300,
      getMember: function() {
        console.log(this, this === company);  // company true
        return this.member;  //  300
      },
      setMember: function(n) {
        console.log(this);
        this.member = n;
      }
    }
    company.getMember(); 

    // this和函数
    function getMember() {
      console.log(this.member);
    }
    var m1 = {
      member: 300
    }
    var m2 = {
      member: 200
    }
    getMember.call(m1); // 300

    // 全局环境的this
    var member = 300;
    function cmpy() {
      console.log(this.member);
    }
    var Company = {
      member: 200,
      getMember: function() {
        console.log(this.member)
      }
    }
    var getMember = Company.getMember;
    cmpy(); // 300
    getMember();  // 300

    // this和DOM事件
    var dom = document.getElementById('dom');
    dom.onclick = function() {
      console.log('this', this); // dom
    }
    function getId() {
      console.log('id', this, this.id); // window
    }

    // this可以被call/apply/bind改变
    var m1 = {
      member: 300
    };
    var m2 = {
      member: 200
    };  
    function showMember() {
      console.log(this.member);
    }  
    showMember(); // undifined
    showMember.call(m1);  // 300
    showMember.apply(m2); // 200
    showMember.bind(m2)();  // 200

    // ES6箭头函数(arrow function)和this 箭头函数的特征就是，定义在哪，this就指向哪。
    var company = {
      name: 'stardew',
      member: 100,
      getMember: function() {
        document.onclick = function () {
          console.log(this, this.member) ;
        }
      }
    }
    company.getMember(); // document undifined

    var company = {
      name: 'stardew',
      member: 100,
      getMember: function() {
        document.onclick = ev => {
          console.log(this, this.member) ;  // conpany 100
        }
      }
    }
    company.getMember();

  </script>
</body>
</html>
```

##### [转自] [详解this](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483773&idx=1&sn=edcd836e97a54132e2397d4c310584f1&chksm=eb02a10bdc75281d1f1180a70b24041d818af7ca58f9571998410d4c2fd49649928cc5809efa&mpshare=1&scene=1&srcid=0628WKgNWbWUhnpBurWBaP3l&key=aa3a7cd9173eb9045c45e29588d3da296a85b1ea5c80f8ac246f12c4db5f324ff9bac341222c6fd94abb1c4a8b56cc2df884bca59c082c21ad651d3bd4cd0f38c5d87031882bf421dc9c1aaf692f46e1&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)