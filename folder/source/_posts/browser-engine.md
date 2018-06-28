---
title: browser-engine
date: 2016/12/11
tags: javascript
categories: 前端基础
---

![](https://mmbiz.qpic.cn/mmbiz_png/0vF1DtfHb3GOYRA04Ftx3MiaoktLhNaxL1zXGTaickibicFvOY1ic0ap6YnOoUXaOrjEBU9fgaSJurvla8ukicEAdVMg/0?wx_fmt=png)

### 一、浏览器内核

    主要指渲染引擎(Rendering Engine)，负责解析网页语法(如HTML、JavaScript)并渲染、展示网页。  

    。Trident内核（代表：Internet Explorer）  

        IE、傲游、世界之窗浏览器、Avant、腾讯TT、Netscape 8、NetCaptor、Sleipnir、GOSURF、GreenBrowser和KKman等。  

    。Gecko内核（代表：Mozilla Firefox）  

        Firefox、Netscape6至9。  

    。WebKit内核（代表：Safari、Chrome）  

    。Presto内核（代表：Opera7）  

    。Elektra内核（代表：Opera4-6）  


### 二、JavaScript引擎

    用来执行JS代码，涉及到跑分。哪个浏览器更快，指JavaScript的渲染速度，而不是页面的载入速度，各个浏览器的页面载入速度差别不大（Opera逊色一些）  

    。Chakra  查克拉  

        IE9启用的新的JavaScript引擎  

    。SpiderMonkey / TraceMonkey / JaegerMonkey
        SpiderMonkey应用在Mozilla Firefox 1.0-3.0，TraceMonkey应用在Mozilla Firefox 3.5-3.6版本，JaegerMonkey应用在Mozilla Firefox 4.0及后续的版本。  

    。V8  

        Chrome、傲游3  

    。Nitro  

        Safari 4及后续的版本  

    。Linear A/Linear B/Futhark/Carakan  
        Linear A应用于Opera 4.0-6.1版本，Linear B应用于Opera 7.0～9.2版本，Futhark应用于Opera 9.5-10.2版本，Carakan应用于Opera 10.5及后续的版本。  

    。KJS  

        KHTML对应的JavaScript引擎  

##### [转自] [浏览器引擎](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483755&idx=1&sn=6e5e73970d332b938cbfce6b8f317032&chksm=eb02a11ddc75280bb64a8eeead14de075e8e85604c56dbac7b37bbb1442fe35f4ac60bba9f41&mpshare=1&scene=1&srcid=0628giv5kvNGsXX0EhkTUjsz&key=aa3a7cd9173eb904ae01e4aa45cf45f6d64e4a580b29b2f48d1a1be02eb477395c8f16dbf84e25ac954a0b8db52a0991f8c9df3ada8364d504140136aa334698fe3de74a92d65383201841d376fb8755&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)