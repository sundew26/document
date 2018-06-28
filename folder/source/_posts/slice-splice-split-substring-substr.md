---
title: slice-splice-split-substring-substr
date: 2017/02/20
tags: javascript
categories: 前端基础
---

# slice，splice，split，substring，substr区别 #

![](https://mmbiz.qpic.cn/mmbiz_jpg/0vF1DtfHb3Fibq2EbGWGYvbPIBNIsInmickdIAeQ0olClsOQlVyTl2BIV1eqzXgicXiaXusPic1HXEIY7bOHibwEYDTw/0?wx_fmt=jpeg)

```
var arr = [1, 3, 5, 7, 9, 2, 4, 6, 8, 1, 2, 3, 4, 5];
var str = '1, 3, 5, 7, 9, 2, 4, 6, 8, 1, 2, 3, 4, 5';
```

### `slice(): slice(i,[j])`  
描述: 截取数组，返回截取的数组，原数组不变  
参数:  
* i: 起始位置（可为负数）  
* j: 可选，结束位置，默认结尾  
```
arr.slice(1, 6)	// [3, 5, 7, 9, 2]
arr.slice(1)	// [3, 5, 7, 9, 2, 4, 6, 8, 1, 2, 3, 4, 5]
arr.slice(-1)	// [5]
arr.slice(-1, 1)	// []
arr.slice(-3, -1)	// [3, 4]
```

### `splice(): splice(i, n, a1, ..., ax)`  
描述: 可删除添加数组，原数组被改变，返回删除的数组  
参数:  
* i: 删除的位置（可为负数）  
* n: 删除数量  
* a1, ..., ax: 添加  
```
arr.splice(3, 4, 5, 6)	// [7, 9, 2, 4]
此时arr: [1, 3, 5, 5, 6, 6, 8, 1, 2, 3, 4, 5]
[1, 3, 5, (删除7, 9, 2, 4) （添加5, 6,） 6, 8, 1, 2, 3, 4, 5]
```

### `split(): split(s, n)`  
描述: 字符串分割为数组  
参数:  
* s: 分隔符  
* n: 分割之后数组的长度  
```
str.split(',')	// ["1", " 3", " 5", " 7", " 9", " 2", " 4", " 6", " 8", " 1", " 2", " 3", " 4", " 5"]
str.split(',', 3)	// ["1", " 3", " 5"]
```

### `substring(): substring(start, stop)`  
描述: 字符串截取  
参数:  
* start: 字符串截取的起始位置  
* stop: 字符串结束位置  
```
str.substring(3, 8)	// "3, 5,"
等价于
str.substring(8, 3)	// "3, 5,"
```

### `substr(): substr(start, length)`  
描述: 字符串截取  
参数:  
* start: 字符串截取的起始位置  
* length: 截取字符串长度  
```
str.substr(3, 8)	// "3, 5, 7,"
```

##### [转自] [slice, splice, split, substring, substr区别](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483780&idx=1&sn=61edd08ed65e29a20b445e68421b45c4&chksm=eb02a1f2dc7528e46569efb9145fc9dbcd840aa387217b4e2e3122eda8c093b3c5f493dc6687&mpshare=1&scene=1&srcid=0628QLDMllnLjDumF6woGRGX&key=aa3a7cd9173eb904b4f6fb7db2efe2f8ac6b5b8b9dbc7dc6f008ac4056af8f714b6ed74a92e95797274fd5d5e565ec97a560d085d7db8c4ea07812c444f147750d8277e00e2ed2eaf4b201262a8db9ee&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)