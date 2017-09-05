1. error(来源: difference-Weex-Vue2-x.md):
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
solution: 页面出现了不能解析的!, 定位到`条件指令	|	if="{{!foo}}"	|	v-if="!foo"`. 页面还存在多处类似问题, 追溯根源是{{引起的, hexo会把{{...}}中的内容作为变量解析,
此时需要转义一下. {转义为`&#123;`, }转义为`&#125;`

此外, ```中的代码也是不会被解析的, 某些情况下可以使用. 例如:

`if="{{foo}}"`  输出 if=""
```
if="{{!foo}}"   输出  if="{{!foo}}"
```

`if="&#123;&#123;!foo&#125;&#125;"`中的大括号不解析, 可是`{`中的又解析.
解决: