---
title: weex-start
date: 2017/07/24
tags: weex
categories: 探索
---

# 我的weex开发之路 #

##### 认识比较浅薄，单纯从使用方面入手，整理了两个半小时，有错误的地方还请指出。

# 1. 构建项目

创建一个项目之前，首先需要选取合适的工具，目前使用比较广的两个weex脚手架有weexpack和weex-toolkit。
#### weex-toolkit（创建的weex项目没有ios和android包）
- weex init weex 创建项目
- 修改weex.html文件，将`./node_modules/weex-vue-render/index.js`修改为`./node_modules/weex-vue-render/dist/index.js`
- cnpm install 加载依赖包
- package.json中的scripts配置`"app": "npm run build & npm run dev & npm run server"`
- npm run app 启动项目

目录结构如下图：
![clipboard.png](https://segmentfault.com/img/bVPAmL)

#### weexpack （创建的weex项目有ios和android包）
- weexpack create weex 创建项目
- weexpack platform add android 添加android
- weexpack platform add ios 添加ios
- weexpack run ios 模拟器运行

目录结构如下图：
![clipboard.png](https://segmentfault.com/img/bVPAly)

因为我们不打包android和ios，只需要将写好的页面打包成.weex.js文件供ios和android开发人员调用，所以采用了weex init的构建方式。

# 2. 工具

#### Weex Devtools

Weex Devtools是Weex开发调试必备的神器，安装好后，终端进入到项目目录，运行weex debug 会自动打开页面

![clipboard.png](https://segmentfault.com/img/bVPAfS)

扫二维码后

![clipboard.png](https://segmentfault.com/img/bVPAgs)

点击Inspector可以看页面信息，我们打开Debugger，然后扫描打包好的js文件二维码就可以开始调试了。

![clipboard.png](https://segmentfault.com/img/bVPAgM)

注： 箭头所指处选debugger，我因为手贱选了个别的，导致好几天console里没有内容提示，还以为版本问题，后来研究了下，发现这里选错了。
# 3. 遇到的问题
> 官方demo跑不通
##### 解决： 
高一点版本的weex-vue-render里index.js路径改变，导致。修改weex.html文件，将`./node_modules/weex-vue-render/index.js`修改为`./node_modules/weex-vue-render/dist/index.js`
> 使用vue-resources获取接口数据, weex web上好的，但是weex-playground中跑不通，一片空白，错误信息：
```
[undefined:344:31] ReferenceError: Can't find variable: document
addStyle
addStylesToDom
exports

__webpack_require__

__webpack_require__

__webpack_require__

__webpack_require__

anonymous
a@main.js:4:16690
main.js:7:8740
```
##### 解决：
weex中不支持document和window，换成其它方式。weex不支持vue-resources，改成weex支持的fetch
> <scroll>里loading一直没效果
##### 解决：
<scroll>中使用refresh就没法用loading，去掉refresh模块
> webpack报错，错误信息 `ERROR in Entry module not found: Error: Cannot resolve 'file' or 'directory' /Users/xx/xx/code/weex/app.js in /Users/xx/xx/code/weex`
##### 解决：
开始一直以为是webpack入口没配置对，检查很多遍，各种测试后，发现这里真的没问题
```
// entry: entries
entry: {
  app: path.resolve('./app.js')
}
```
后来找到问题出自
```
resolve: {
  extensions: ['.js', '.vue', '.json']
},
```
原因是修改了默认的这个配置后，第一个空项不能省略，应该配置为
```resolve: {
  extensions: ['', '.js', '.vue', '.json']
},
```
> 错误信息 `Cannot resolve module 'sass-loader'`
##### 解决：
缺少node-sass 或 sass-loader
`npm install node-sass sass-loader --save-dev`
把sass-loader安装成了"scss-loader": "0.0.1",也是服了我自己。
> 接口地址只能获取本地数据，配置test环境失败
##### 解决：
server.js中加一层代理
```
require('http-proxy-middleware')

// api代理
var proxyTable = config.test.proxyTable
Object.keys(proxyTable).forEach(function (context) {
  var options = proxyTable[context]
  if (typeof options === 'string') {
    options = { target: options }
  }
  server.use(proxyMiddleware(context, options))
})

// proxyTable数据
proxyTable: {
  '/api': {
    // 测试服务器
    target: 'http://ip地址:端口号/xx',
    changeOrigin: true,
    pathRewrite: {
      '^/api': ''
    }
  },
  ...
}
```
> weex接口调用，fetch的headers某些字段始终设置不上
##### 解决：
fetch的headers只能设置下面这些字段
参考： https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS
***
  ● 人为设置了对CORS安全的首部字段集合之外的其他首部字段。该集合为：
    ○ Accept
    ○ Accept-Language
    ○ Content-Language
    ○ Content-Type (but note the additional requirements below)
    ○ DPR
    ○ Downlink
    ○ Save-Data
    ○ Viewport-Width
    ○ Width
  ●  Content-Type 的值不属于下列之一:
    ○ application/x-www-form-urlencoded
    ○ multipart/form-data
    ○ text/plain
***
> stream的fetch使用get方式请求接口，url都会自动加上&undefined，官网的例子也不例外。原本普通接口多加一个undefined也没太大影响，但是我们项目是需要根据url参数计算签名的，所以一直签名不通过。

![clipboard.png](https://segmentfault.com/img/bVPAyC)

##### 解决：

找到源码出处
![clipboard.png](https://segmentfault.com/img/bVPz7b)
![clipboard.png](https://segmentfault.com/img/bVPz6u)
![clipboard.png](https://segmentfault.com/img/bVPABE)

weex-vue-render第2753行对get进行了特别处理，第2764行的url拼接了body和hash，因为body没有传值，所以是undefined，注释掉url+=这行就没有undefined了，但是修改node_modules中的包内容显然不是一个合理的解决方案。
于是把get方式传值改为body传过来，web端好了，签名没有问题，但是真机上还是报错，排查后发现问题出在get中使用了body传值，找到开发文档，
http://weex.apache.org/cn/references/modules/stream.html
![clipboard.png](https://segmentfault.com/img/bVPABf)
然后我凌乱了，为什么明明不能传body你的源码里又要有那么一行代码`url += (config.url.indexOf('?') <= -1 ? '?' : '&') + body + hash;`。没办法，最后使用了一个超级笨的办法解决了。在签名计算的时候人为的给url加上“&undefined",计算好签名后，web中fetch参数中的url也要加上“&undefined"，但是真机上是不会有&undefined的，所以真机上的url需要去掉undefined，好了问题解决了。

> storage中的`getItem(key, callback)`封装后，页面没拿到数据。
##### 解决：
storage异步造成的，使用promise解决
```
const p1 = new Promise(function (resolve) {
    storage.getItem(key, event => {
      let ls = event.data || ''
      let d = secret.decrypt(ls) // 对密文字符串进行解密。
      d = typeof d === 'object' ? JSON.parse(d) : d
      resolve(d)
    })
  })
  Promise.all([p1]).then(function (result) {
    callback(result)
  }).catch(function(err){
    console.log('error', err)
  })
```
> 页面跳转外部非js链接，在网页上是好的，但真机上一片空白
```
navigator.push({
  url: 'https://segmentfault.com/write?freshman=1',
  animated: "true"
})
```
##### 解决：
新建一个vue文件，使用weex的web标签包一层，然后打包成weex.js格式，普通调用就好了。
`<web class="content" :src="url"></web>`
> 跳转weex.js页面传参
##### 解决：
直接在url后面拼接参数，新页面使用this.$getConfig().bundleUrl获取url解析一下就好了。
> post提交数据的是后报错415
##### 解决：
头部信息一定要和后端协议好，不允许不一致。

##### [转自] [我的weex开发之路](https://segmentfault.com/a/1190000009873690)