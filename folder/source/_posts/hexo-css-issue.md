---
title: hexo-css-issue
date: 2017/09/06
tags: javascript
---

### 问题背景
使用hexo+css模拟实现weex文档，页面[Weex 和 Vue 2.x 的语法差异][1]遇到问题。
### 问题描述
新建页面，copy进去内容，hexo server运行，控制台报错：
```
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Template render error: (unknown path) [Line 17, Column 9]
  unexpected token: !
    at Object.exports.prettifyError (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/nunjucks/src/lib.js:34:15)
    at Obj.extend.render (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/nunjucks/src/environment.js:469:27)
    at Obj.extend.renderString (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/nunjucks/src/environment.js:327:21)
    at /Users/weilu/Desktop/weilu/code/document/folder/node_modules/hexo/lib/extend/tag.js:66:9
    at Promise._execute (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/debuggability.js:300:9)
    at Promise._resolveFromExecutor (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/promise.js:483:18)
    at new Promise (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/promise.js:79:10)
    at Tag.render (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/hexo/lib/extend/tag.js:64:10)
    at Object.tagFilter [as onRenderEnd] (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/hexo/lib/hexo/post.js:266:16)
    at /Users/weilu/Desktop/weilu/code/document/folder/node_modules/hexo/lib/hexo/render.js:65:19
    at tryCatcher (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/util.js:16:23)
    at Promise._settlePromiseFromHandler (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/promise.js:512:31)
    at Promise._settlePromise (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/promise.js:569:18)
    at Promise._settlePromise0 (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/promise.js:614:10)
    at Promise._settlePromises (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/promise.js:693:18)
    at Async._drainQueue (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/async.js:133:16)
    at Async._drainQueues (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/async.js:143:10)
    at Immediate.Async.drainQueues (/Users/weilu/Desktop/weilu/code/document/folder/node_modules/bluebird/js/release/async.js:17:14)
    at runCallback (timers.js:574:20)
    at tryOnImmediate (timers.js:554:5)
    at processImmediate [as _immediateCallback] (timers.js:533:5)
```
### 定位问题
问题定位到`if="&#123;&#123;!foo&#125;&#125;"`这句文案。文档中的效果如下：

![clipboard.png](https://segmentfault.com/img/bVUuMg)


### 分析问题：
报错信息写的很明确，`unexpected token: !`，!是不被期望的。其实这是因为使用了`&#123;&#123;...&#125;&#125;`导致的，在hexo中双括号会被解析，双括号里的内容会被当做变量解析。
### 解决问题
以下是几种可能的解决方案
1. 网上找到方法说使用&#39;可以不解析&#123;&#123;，其实不然，使用&#39;后会不解析转义后的特俗字符，例如改为
    ```
    `if="&#125;&#125;!foo&#125;&#125;"`
    还是会解析，会报同样的错误，所以`包裹是不能解决问题的。
    ```
2. 还有的是说使用&#39;&#39;&#39;三个反引号，三个&#39;&#39;&#39;确实可以解决解析方面的问题，但是不能解决我们这里的问题，我们看文档可以知道，这句`if="&#123;&#123;!foo&#125;&#125;"`是在表格中的，而&#39;&#39;&#39;生成的是代码块，所以三个反引号是不能最终解决问题的。
    
3. 转义。一般很多类似`unexpected token: ***`的问题，都可以使用转义的方法解决，关于转义字符，可以看我上一篇文章[hexo+css创建自己的blog（语法手册）][2]，里面最底下有各种特殊字符对应的转义码。以下是我解决问题的三个过程：

    ```
    `if="&#123;&#123;!foo&#125;&#125;"`
    这种方式时，`根本不会把转义过后的内容反转义回去，效果图如下图1。
    
    图1的效果并不是我们期望的，只是我们知道`最终在页面展示的效果是包裹在code中的，所以我们可以用如下方式，效果如下图2。
    <code>if="&#123;&#123;!foo&#125;&#125;"</code>
    
    图2中可以看出，双引号变成了中文的，这也不是我们期望的，需要转义一下，改为如下方式，完美解决问题，结果如图3。
    <code>if=&quot;&#123;&#123;!foo&#125;&#125;&quot;</code>
    ```
图1：
![clipboard.png](https://segmentfault.com/img/bVUuEK)

图2：
![clipboard.png](https://segmentfault.com/img/bVUuGL)

图3：
![clipboard.png](https://segmentfault.com/img/bVUuFi)

### 总结
使用hexo创建博客写文章的时候，遇到的问题几乎都是特殊字符解析方面的问题，所以应该尽可能少写一些特殊字符，如果实在需要，可以使用转义码。遇到问题时，解决思路可以考虑下转义码+html标签。

  [1]: http://weex.apache.org/cn/references/migration/difference.html
  [2]: https://segmentfault.com/a/1190000011021195


##### [转自] [hexo+css遇到的unexpected token问题](https://segmentfault.com/a/1190000011042242)