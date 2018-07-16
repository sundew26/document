---
title: vueresource-405
date: 2017/07/25
tags: vue
categories: 问题总结
---

# vue-resource报错450的解决方案 #

vue-resource(github)地址：https://github.com/pagekit/vue-resource

一、基本使用
-------

##### 1.页面引入
```
  import vueResource from 'vue-resource'
  Vue.use(vueResource)
```
 <!-- more -->
##### 2. 调取接口
```
Vue.http.post(url, {
  'data1': data1,
  'data2': 'data2'
}).then(response => {
  console.log('success', response)
}, response => {
  console.log('error', response)
})
```

二、报错450
-------

定位错误信息：请求header没有完全一一对应。`Content-Type: application/x-www-form-urlencoded; charset=UTF-8`应为`Content-Type: application/json; charset=UTF-8`，检查页面代码，发现已经设置了
```
Vue.http.interceptors.push(function (request, next) {
  request.headers.set('Content-Type', 'application/json; charset=UTF-8')
  request.headers.set('Content-Type', 'application/json')
  next()
})
```
只是页面没有起作用而已，那究竟是什么原因导致页面设置的Content-Type失效了呢？继续追溯，发现跟这行代码有关
```
  // Vue.http.options.crossOrigin = true 
  // Vue.http.options.emulateHTTP = true
  Vue.http.options.emulateJSON = true //（跟这行代码有关）

```

三、分析
----

下面分别来讲一下这几行代码的用处，以及emulateJSON是怎么影响到Content-Type设置的。
##### 1. Vue.http.options.crossOrigin
这个很明显是设置跨域的，此处不多讲。
##### 2. Vue.http.options.emulateHTTP
参考地址：https://github.com/pagekit/vue-resource/blob/develop/src/http/interceptor/method.js
摘出源码
```
/**
 * HTTP method override Interceptor.
 */

export default function (request, next) {

    if (request.emulateHTTP && /^(PUT|PATCH|DELETE)$/i.test(request.method)) {
        request.headers.set('X-HTTP-Method-Override', request.method);
        request.method = 'POST';
    }

    next();
}
```
大概的意思就是如果请求方式为PUT|PATCH|DELETE，服务器又没法处理这几类请求的时候，设置`Vue.http.options.emulateHTTP = true`的话可以将X-HTTP-Method-Override设置为PUT|PATCH|DELETE，然后使用普通的post进行请求。
关于X-HTTP-Method-Override讲一下，它的使用场景是：
在某些HTTP代理不支持类似PUT|PATCH|DELETE这些类型HTTP请求的情况下，可以通过另一种完全违背协议的HTTP方法来"代理"。这种协议就是，使客户端发出HTTP POST请求并设置header里X-HTTP-Method-Override值为PUT|PATCH|DELETE。

##### 3. Vue.http.options.emulateJSON

参考地址：https://github.com/pagekit/vue-resource/blob/develop/src/http/interceptor/form.js
摘出源码
```
/**
 * Form data Interceptor.
 */

import Url from '../../url/index';
import { isObject, isFormData } from '../../util';

export default function (request, next) {

    if (isFormData(request.body)) {

        request.headers.delete('Content-Type');

    } else if (isObject(request.body) && request.emulateJSON) {

        request.body = Url.params(request.body);
        request.headers.set('Content-Type', 'application/x-www-form-urlencoded');
    }

    next();
}

```
从第17行可以看到，如果设置了emulateJSON的话会默认加上这句
```
request.headers.set('Content-Type', 'application/x-www-form-urlencoded');
```
这就是为什么我们设置的Content-Type失效了。只要去掉Vue.http.options.emulateHTTP = true 或者直接置为false就可以了。

##### [转自] [vue-resource报错450的解决方案](https://segmentfault.com/a/1190000010321126)