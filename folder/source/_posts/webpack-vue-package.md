---
title: webpack-vue-package
date: 2016/10/06
tags: tools
categories: 工具类
---

## webpack + vue 开发涉及到的包

1、crypto-js
- 纯javascript写的加密算法类库，包括 MD5 SHA-1 SHA-256 AES Rabbit MARC4 HMAC (HMAC-MD5 HMAC-SHA1 HMAC-SHA256) PBKDF2

---
<!-- more -->
2、es6-promise
- 轻量级库，用于组织异步代码的工具
- ES6 Promise 的 polyfill（见附件）

---

3、js-md5
- 一个支持utf-8编码的简洁md5哈希算法方法

---

4、node-sass
- 一个库
- 把node绑定到libsass（见附件）

---

5、prompt
- 终端命令行输入控件
- 可根据用户输入的信息做相应的操作

---

6、sass-loader
- webpack中将sass转化为模块

---

7、vue
- 一个构建数据驱动的 web 界面的库
- 提供了 MVVM 数据绑定和一个可组合的组件系统，API简单、灵活

---

8、vue-drag-and-drop
- vue拖拽组件

---

9、vue-resource
- vue-resource类似jQuery里的$.ajax
- 用来和后端交互数据

---

10、vue-router
- Vue官方路由插件

---

11、vuex
- 一个专门为 Vue 应用设计的状态管理架构

---

12、vux
- 基于vue和weui的组件库

---

13、babel-core
- babel是一个转码器，可以将es6转为es5
- babel-cli是babel的一个工具，用于命令行转码
- babel-core是babel的一个api库，转码时需要引入

---

14、babel-loader
- webpack中将babel转化为模块

---

15、babel-plugin-transform-runtime
- 替换助手函数
- 包括部分es6的API， 但是某些情况不会替换
- 帮助用户和构建者的一个外部引用，在不污染全局的情况下自动补全代码

---

16、babel-preset-es2015
- 为babel预置所有es2015插件

---

17、babel-preset-stage-2
- 为babel预置stage-2插件

---

18、babel-polyfill
- babel 虽然可以转换各种 ES2015 语法及 jsx，但浏览器未提供原生支持的许多功能还是需要 polyfill，比如 Promise。
- 针对全局

---

19、babel-runtime
- 为了减少重复代码而生
- 将一些重复工具函数的代码转换成require语句，指向为对babel-runtime的引用，此代码就不需要在每个文件中都存在了。

---

20、chai
- node和浏览器的BDD/TDD断言库
- 可以友好的和javascript测试框架配对使用

---

21、chromedriver
- Selenium chromedriver的一个npm包装器
- chrome测试时需要用到
- Chrome的WebDriver，可以用于自动化测试，可以操作浏览器

---
 
22、connect-history-api-fallback
- 对不存在的目录提供回退功能，使得html5 的历史api可以使用
- 用于支持HTML5 history API
- 单页应用回退功能
- 用于匹配资源

---
 
23、cross-spawn
- Cross platform child_process#spawn and child_process#spawnSync

---
 
24、css-loader
- webpack中将css转化为模块

---
 
25、eslint
- 一个QA工具
- 用来避免低级错误和统一代码的风格
- ESLint被设计为完全可配置的

---

26、eslint-config-standard
- eslint校验的标准配置

---

27、eslint-friendly-formatter
- eslint友好支持sublime
- 错误结果展示界面友好

---

28、eslint-loader
- webpack中将eslint转化为模块

---

29、eslint-plugin-html
- ESLint插件，用于从HTML文件中提取和删除脚本

---

30、eslint-plugin-promise
- JavaScript promises的最佳实现

---

31、eslint-plugin-standard
- Linter的eslint插件

---

32、eventsource-polyfill
- 支持w3c规范, 一个浏览器w3c eventsource的ployfill, 在不支持事件源的浏览器里添加填充策略支持
- 先检查浏览器是否支持某个api, 如果不支持就加载对应的polyfill

---

33、express
- 基于Node.js 平台,快速、开放、极简的 web 开发框架
- 一系列middleware的集合

---

34、extract-text-webpack-plugin
- 把css打包成独立的文件 样式通过&lt;link&gt;引入，而不是放在&lt;style&gt;标签内

---

35、file-loader
- webpack中将file转化为模块

---

36、glob
- 使用类似shell的模式匹配文件，如‘ * ’和‘ ... ’

---

37、html-webpack-plugin
- 服务于webpack包的简化html文件创建的插件

---

38、http-proxy-middleware
- 代理中间件 for (connect, express, browser-sync)

---

39、json-loader
- webpack中将json转化为模块

---

40、karma
- JavaScript的测试运行器
- 使我们的javascript代码可以在多个实际的浏览器上执行

---

41、karma-coverage
- karma插件，用于生成代码覆盖

---

42、karma-mocha
- karma插件，Mocha测试框架的适配器

---

43、karma-phantomjs-launcher
- Karma插件，PhantomJS的启动器

---

44、karma-sinon-chai
- Sinon and Chai for Karma

---

45、karma-sourcemap-loader
- Karma插件，用于定位和加载现有的JavaScript的sourcemap文件

---

46、karma-spec-reporter
- karma插件，把所有spec-results打印到控制台
- 类似mocha的spec report

---

47、karma-webpack
- webpack中载入karma

---

48、less
- css增强版

---

49、less-loader
- webpack中将less转化为模块

---

50、mocha
- 简单，灵活，有趣的测试框架

---

51、nightwatch
- 一套新近问世的基于Node.js的验收测试框架
- 使用Selenium WebDriver API以将Web应用测试自动化

---

52、ora
- 终端精致的旋转loading...插件

---

53、selenium-server
- 主要控制浏览器行为

---

54、shelljs
-  Node.js 扩展，用于实现 Unix shell 命令执行

---

55、sinon
- 一套面向js的单元测试辅助库
- 监听，存根，模拟
- 一个独立的 JavaScript 测试间谍，没有依赖任何单元测试框架工程。

---

56、sinon-chai
- 通过断言为sinon扩展chai
- js的模拟框架

---

57、stylus
- 强大，富有表现力，功能丰富的CSS超集

---

58、stylus-loader
- webpack中将stylus转化为模块

---

59、url-loader
- webpack中将url转化为模块

---

60、vue-hot-reload-api
- *.vue 组件的热加载api

---

61、vue-html-loader
- webpack中将vue template转化为模块

---

62、vue-loader
- webpack中将vue component转化为模块

---

63、vue-style-loader
- webpack中将vue style转化为模块

---

64、webpack
- 前端资源模块化管理和打包工具
- 可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源
- 还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载
- 通过 loader 的转换，任何形式的资源都可以视作模块
- 为浏览器打包CommonJs / AMD模块
- 可以将你的代码库拆分为多个包，实现按需加载
- 支持加载器预处理文件，如json, jsx, es7, css, less, ... 或者是自定义的内容

---

65、webpack-dev-middleware
- 组织包装webpack的中间件

---

66、webpack-dev-server
- 为webpack服务的一个应用
- 在更改时更新浏览器

---

67、 webpack-hot-middleware
- 热部署，可以连到自己的服务器上
- 需要用到webpack-dev-server

---

68、webpack-merge
- 合并webpack配置 可以是 array 或 object

---

69、html-webpack-plugin-after-emit
- html-webpack-plugin允许其它是插件去执行事件

---

###  附件
1、shim
- 一个库，目的是解决浏览器的兼容性问题
- 将一个新的环境引入到一个旧的环境中, 而且仅靠旧环境中已有的手段实现

---

2、polyfill
- 切确说是一种概念，目前弄成库而已，可以理解是shim的集合
- 一个用在浏览器API上的shim
- 形象的例子：旧的shim好比一面墙, 这面墙有些裂缝, polyfill能磨平裂缝
- 实际的例子：bind 函数在 ECMA-262 第五版才被加入，有些旧版本浏览器上无法直接使用bind()功能，需要在顶部加入以下代码。
```
if (!Function.prototype.bind) {
  Function.prototype.bind = function (oThis) {
    if (typeof this !== "function") {
      throw new TypeError("Function.prototype.bind - what is trying to be bound is not callable");
    }
    var aArgs = Array.prototype.slice.call(arguments, 1), 
    fToBind = this, 
    fNOP = function () {},
    fBound = function () {
      return fToBind.apply(this instanceof fNOP ? this : oThis || this, aArgs.concat(Array.prototype.slice.call(arguments)));
    };
    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();
    return fBound;
  }
}
```

---

3、sass
- 一个流行的客户端版的样式预处理器

---

4、libsass
- sass 是用ruby写的
- Sass引擎的一套 C/C++ 接口实现，所以可以很简单、方便、快速的集成到其它语言中
- 本身不做任何事，它只是一个库
- 需要类似node-sass这一类包装器的支持
- 速度比ruby sass 快了4000%倍
- 缺点是暂时缺失小部分sass功能

---

5、Ruby Sass
- 离开ruby sass无法运行
- 编译时间比较久

---

6、Selenium
- 自动化测试工具
 
自己闲暇时间整理了一份项目里用到的包，请大家纠错。

##### [转自] [webpack + vue 开发涉及到的包](https://cnodejs.org/topic/5810631b1a9a7d9909531159)