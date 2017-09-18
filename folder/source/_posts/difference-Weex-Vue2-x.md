---
title: difference-Weex-Vue2-x
date: 2017-09-01 16:47:27
tags: vue
---

## Weex 和 Vue 2.x 的语法差异
###### Updated time: 14/06/2017

### Overview

  | Weex | Vue
 ----- | ----- | -----
生命周期	|	`ready: function() {}` | `mounted: function() {}`
条件指令	|	<code>if=&quot;&#123;{!foo}}&quot;</code>	|	`v-if="!foo"`
循环指令	|	<code>repeat=&quot;&#123;{item in list}}&quot;</code>	|	`v-for="item in list"`
样式类名	|	<code>class=&quot;btn btn-&#123;{type}}&quot;</code>	|	`:class="['btn', 'btn-' + type]"`
内联样式	|	<code>style=&quot;color:&#123;{textColor}}&quot;</code>	|	`:style="{ color: textColor }"`
事件绑定	|	`onclick="handler"`	|	`@click="handler"`
原生事件	|	`onclick="xxx"`	|	`@click.native="xxx"`
数据绑定	|	<code>src=&quot;&#123;{rightItemSrc}}&quot;</code>	|	`:src="rightItemSrc"`
内容/槽	 | `<content></content>`	|	`<slot></slot>`
数据初始化 |	`data: { value: 'x' }`	|	`data: function() { return { value: 'x' } }`
标签 ID	|	`id="xxx"`	|	`ref="xxx"`
获取节点	|	`this.$el('xxx')`	|	`this.$refs.xxx`

### Reference
See the source code of `weex-vue-migration` for more details:

* [template-rewriter](https://github.com/songsiqi/weex-vue-migration/blob/master/src/template-rewriter/rewriter.js)
* [script-rewriter](https://github.com/songsiqi/weex-vue-migration/blob/master/src/script-rewriter/rewriter.js)

### LifeCycle Hooks 生命周期钩子

weex | vue | Description
--- | --- | ---
init | beforeCreate | 组件实例刚刚被创建，组件属性如data计算之前
created | created | 组件实例创建完成，属性已绑定，但DOM还未生成
 | beforeMount | 模板编译/挂载之前
ready | mounted | 模板编译/挂载之后
 | beforeUpdate | 组件更新之前
 | updated | 组件更新之后
 | activated | for `keep-alive`, 组件被激活时调用
 | deactivated | for `keep-alive`, 组件被移除时调用
 | beforeDestroy | 组件被销毁前调用
destroyed | destroyed | 组件被销毁后调用

在weex中，使用&#123;{…}}在`<template>`中绑定在`<script>`里定义的数据；在vue中，需要在要绑定的属性前加 `:` 。如以下示例。

* 类名

  * weex
  ```
  <div class="btn btn-&#123;{type}}"></div>
  ```
  * vue
  ```
  <div :class="['btn', 'btn-' + type]"></div>
  ```
* 样式绑定
  * weex
  ```
  <div style="color:{{textColor}}"></div>
  ```
  * vue
  ```
  <div :style="{color: textColor}"></div>
  ```
* weex
  ```
  <image src="..." if="{{shown}}"></image>
  ```
    or
  ```
  <image src="..." if="shown"></image>
  ```
* vue
  ```
  <image src="..." v-if="shown"></image>
  ```
* weex: repeat
  * `$index`为索引
  ```
  <div repeat="{{list}}">
    <text>No. {{$index + 1}}</text>
  <div>
  ```
    or
  ```
  <div repeat="{{v in list}}">
    <text>No. {{$index + 1}}, {{v.nickname}}</text>
  </div>
  ```
  * 对象参数的顺序
  ```
  <div repeat="{{(key, value) in list}}">
    <text>No. {{key + 1}}, {{value.nickname}}</text>
  </div>
  ```
  * `track-by`
  ```
  <div repeat="{{item in items}}" track-by="item.id" class="{{gender}}"></div>
  ```
* vue: v-for

  * 移除`$index`索引

  * 对象参数的改变：改为(value, key), 与通用的对象迭代器保持一致
  ```
  <div repeat="{{(value, key) in list}}">
   <text>No. {{key + 1}}, {{value.nickname}}</text>
  </div>
  ```
  * `track-by` 替换为`v-bind`
  ```
  <div v-for="item in items" v-bind:key="item.id">
  ```
* weex
```
data: { value: 'x' }
```
* vue
```
props: { value: { default: 'x' } }
```
动态数据
```
data: function () { return { value: 'x' } }
```
* 获取节点

  * weex: `this.$el('xxx')`
  ```
  <template>
   <container>
    <text id="top">Top</text>
   </container>
  </template>
  <script>
  module.exports = {
    methods: {
      toTop: function () {
        var top = this.$el('top')
      }
    }
  }
  </script>
  ```
  * vue
  ```
  this.$refs.xxx
  ​```

* 事件绑定

  * weex
  ```
  <div onclick="handler"></div>
  ```
  * vue
  ```
  <div @click="handler"></div>
  ```
* 事件触发
  * weex: dispatch和broadcast
  ```
  this.$dispatch()
  ```
    ```
    this.$broadcast()
    ```
  * vue: emit
  ```
  this.$emit()
  ```
  > 注：Weex 的 `$dispatch` 与组件无关，在任意组件中都可以通过 `$on` 捕获到，Vue 的`$emit` 用于触发组件(标签)的自定义事件。

* 原生事件

  * weex
  ```
  onclick="xxx"
  ```
  * vue
  ```
  @click.native="xxx"
  ```