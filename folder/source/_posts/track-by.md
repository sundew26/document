---
title: track-by
date: 2016/10/25 16:20
tags: vue
---

## vue中track-by的理解

api：[http://cn.vuejs.org/guide/list.html#track-by](http://cn.vuejs.org/guide/list.html#track-by)

示例地址：[https://jsfiddle.net/stardew/f1eju0ku/5/](https://jsfiddle.net/stardew/f1eju0ku/5/)

无track-by情况：数据修改时，无论值是否被修改，dom都被重新渲染（控制台可以看到）

加入track-by属性：数据修改时，不变数据所在的dom不被重新渲染，已改变的数据所在dom才被重新渲染

track-by的两种使用方法：

### 1\. 使用数据中某唯一字段，例如_uid

```html
<div  id="example">
  <p v-for="item in items" track-by="_uid">
    {{item.message}}
  </p>
  <input type="button" value="修改" @click="modify"/>
  <input type="button" value="还原" @click="reduct"/>
</div>
```

```javascript
// 初始数据
items: [
  { _uid: '111111', message: '111' },
  { _uid: '222222', message: '222' },
  { _uid: '333333', message: '333' },
  { _uid: '444444', message: '444' },
  { _uid: '555555', message: '555' }
]
```

```javascript
// 修改成
modify: function () {
  this.items = [
    { _uid: '111111', message: '111' },
    { _uid: '666666', message: '222' },
    { _uid: '333333', message: '3333' },
    { _uid: '888888', message: '4444' },
    { _uid: '999999', message: '5555' }
  ]
}
```

渲染效果如下图右(左边无track-by，右边有track-by)，_uid和message都不变的情况下，才不被重新渲染，只有第一组符合条件。

![](http://static.oschina.net/uploads/space/2016/1025/160552_0PEU_255575.png)![](http://static.oschina.net/uploads/space/2016/1025/155631_7GXl_255575.png)

### 2\. 使用$index，其它条件同上

```html
<div  id="example">
  <p v-for="item in items" track-by="$index">
    {{item.message}}
  </p>
  <input type="button" value="修改" @click="modify"/>
  <input type="button" value="还原" @click="reduct"/>
</div>
```

渲染效果如下图右，message的值第一、二条都没改变，所以一、二都没有重新渲染。

![](http://static.oschina.net/uploads/space/2016/1025/160552_0PEU_255575.png)![](http://static.oschina.net/uploads/space/2016/1025/161002_B1YX_255575.png)

模板中同时使用message和_uid时，只有两者都不变的情况下才不重新渲染，如下：

```html
<div  id="example">
  <p v-for="item in items" track-by="$index">
    {{item.message}}  {{item._uid}}
  </p>
  <input type="button" value="修改" @click="modify"/>
  <input type="button" value="还原" @click="reduct"/>
</div>
```

![](http://static.oschina.net/uploads/space/2016/1025/160552_0PEU_255575.png)![](http://static.oschina.net/uploads/space/2016/1025/161456_wP59_255575.png)

##### [转自] [vue中track-by的理解](https://my.oschina.net/luweiweiwei/blog/775534)