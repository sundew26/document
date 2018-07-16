---
title: vue-drag-and-drop
date: 2016/09/21 11:59
tags: vue
categories: 小例子
---

## 输入内容转图片（vue + html2canvas + vue-drag-and-drop）

最近做了一个小工具，把输入的内容转成图片输出。使用插件 html2canvas，vue-drag-and-drop  

功能：输入列表框可上下移动、拖拽、添加、删除，生成图片可预览、下载。  

基本思路：把html转成canvas，然后把canvas存成图片。  
 <!-- more -->
完成：用插件vue-drag-and-drop，使输入列表可拖拽；刚开始自己根据输入的内容用canvas画图，但是考虑到可扩展性，最后选择html2canvas工具把html转成canvas。  

遇到的问题及解决办法：  

### 1\. 开始自己根据输入所得数据用canvas一行一行画，文字断行处右边对不齐。  

#### 问题成因：因为输入的文字有中文英文等，占位不同，固定每行截取字符的长度导致右端不对齐。  

#### 解决：所有文字都转为英文字符数，中文占两字符，其它占一个字符，计算出行数；每行英文字符占位是固定的x，然后从开始位置往后计算x长度时，正常文字所在位置，substr截取出来，canvas画上。  
```
// 获取段落真实长度,包括中英文
getTrueLength: function (str) {
  let len = str.length
  let truelen = 0
  for (let x = 0; x < len; x++) {
    if (str.charCodeAt(x) > 128) {
      truelen += 2
    } else {
      truelen += 1
    }
  }
  return truelen
},
// canvas画图时,文字切割
cutString: function (str, leng) {
  let len = str.length
  let tlen = len
  let nlen = 0
  for (let x = 0; x < len; x++) {
    if (str.charCodeAt(x) > 128) {
      if (nlen + 2 < leng) {
        nlen += 2
      } else {
        tlen = x
        break
      }
    } else {
      if (nlen + 1 < leng) {
        nlen += 1
      } else {
        tlen = x
        break
      }
    }
  }
  return tlen
},
```

### 2\. textarea里输入的换行、空格直接存到所需样式的div里时，没效果。  

#### 问题成因：编码格式不统一，textarea内容存到textarea里格式是一致的。  

#### 解决：转义一下，空格替换成&nbsp;换行\r\n换为`<br>`，template里使用&#123;&#123;&#123;&#125;&#125;&#125;而非&#123;&#123;&#125;&#125;解析。  

```
nl2br: function (str, idx, tag, isXhtml) {
  let blankTag = '&nbsp;'
  let breakTag = (isXhtml || typeof isXhtml === 'undefined') ? '<br />' : '<br>'
  let newStr = (str + '').replace(/([^>\s]?)(\s)/g, '$1' + blankTag + '$2')
  newStr = (newStr + '').replace(/([^>\r\n]?)(\r\n|\n\r|\r|\n)/g, '$1' + breakTag + '$2')
  if (tag) {
    this.changeData[idx][tag] = newStr
  }
  return newStr
},
```

### 3\. 画成的canvas，存成图片模糊。

#### 问题成因：屏幕显示和屏幕像素一样大小的图片时，尺寸相符，一个屏幕像素对应一个图像像素，显示清晰，但是一个比屏幕像素小的图片展示时，屏幕像素比图片像素多，一个图片像素要用一个多屏幕像素来显示，此时，图像显示驱动的平滑处理功能生效，显示驱动用插值算法在源图中扩展生成新的像素点，图片被拉伸，所以模糊了。  

#### 解决：知道了问题的成因就好办了，可是把canvas画大一点，图片比屏幕大了就不会模糊了，简单的解决办法是使用双倍canvas高宽，画成图，toDataUrl转成.jpg图片，然后图片展示时缩放一倍。 = > canvas width 1960，img width: 980  

```
// 文本信息保存成图片
saveImageInfo: function () {
  let mycanvas = document.getElementById('canvas')
  let image = mycanvas.toDataURL('image/png')
  let w = window.open('about:blank', 'image from canvas')
  w.document.write('<img src="' + image + '" alt="from canvas" style="width: 980px; margin: 0 auto; display: block; height: ' + (this.canvasHeight / 2) + 'px"/>')
},
// 存为本地图片
saveAsLocalImage: function () {
  let myCanvas = document.getElementById('canvas')
  let image = myCanvas.toDataURL('image/png').replace('image/png', 'image/octet-stream')
  window.location.href = image
},
```

### 4. html2canvas把html页面存成图片时，图片不全。

#### 问题成因：html2canvas只能把当前浏览器窗口内及以下部分的内容转成图片，任何已经滚动到浏览器顶部以上以及position、fixed后的非可视的内容都无法存图  

#### 解决办法：先记录当前scrollTop值，window.scrollTo(0,0)到顶部，然后画图，就可以解决了，完了再回到原来的scroll位置。  

```
// 文本信息画成canvas
draw: function (callback) {
  let y = document.body.scrollTop || document.documentElement.scrollTop || 0
  window.scrollTo(0, 0)
  window.html2canvas(document.querySelector('#drawImg'), {allowTaint: false, taintTest: false}).then(function (canvas) {
    this.ob.innerHTML = ''
    this.ob.appendChild(canvas)
    window.scrollTo(0, y)
    callback && callback()
  }.bind(this))
},
```

### 5. html2canvas画出来的图片也模糊。

#### 问题成因：如3  

#### 解决：因为插件里的内容别的地方可能也要用，所以不修改canvas画布大小的算法。画布的大小是所要画的html内容决定的，所以只要这个html整体放大一倍，图片再缩小一倍就可以解决了。  

##### [转自] [输入内容转图片（vue + html2canvas + vue-drag-and-drop）](https://my.oschina.net/luweiweiwei/blog/749569)