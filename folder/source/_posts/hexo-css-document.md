---
title: hexo-css-document
date: 2017/09/05
tags: blog
categories: 博客
---

## hexo语法使用手册 ##

注意：因语法问题，有些hexo的效果在segmentfault中无法正常显示。

### 1. 列表

```
有序号:
1. 第一点
2. 第二点
3. 第三点

无序号:
* 星号列表
+ 加号列表
- 减号列表
```
 <!-- more -->
效果:
1. 第一点
2. 第二点
3. 第三点
* 星号列表
+ 加号列表
- 减号列表


### 2. 块注释

```
> 区块引用

或者:
{% blockquote %}
普通的引用
{% endblockquote %}

嵌套引用
> 一层引用
>> 两层引用
```
效果:
> 区块引用

注：blockquote效果不显示
{% blockquote %}
普通的引用
下一行
{% endblockquote %}

> 一层引用
>> 两层引用
>


### 3. 分割线

```
***
---
```
效果:

***
---


### 4. 链接
```
[这是一个绝对路径的链接](https://hexo.io/zh-cn/docs/writing.html)
[这是一个相对路径的链接](/document/2017/08/07/hello-world/)
{% link text url [external] [title] %}
你好,我是{% link 百度 https://www.baidu.com/ 搜索  度娘 %}.
```
效果：
[这是一个绝对路径的链接](https://hexo.io/zh-cn/docs/writing.html)
[这是一个相对路径的链接](/document/2017/08/07/hello-world/)

注：效果不显示
你好,我是{% link 百度 https://www.baidu.com/ 搜索  度娘 %}.

### 5. 加粗

```
**双星加粗**
__双下划线加粗__
```
效果：
**双星加粗**
__双下划线加粗__


### 6. 斜体

```
*星号斜体*
_下划线斜体_
```
效果：
*星号斜体*
_下划线斜体_



### 7. 图片

```
![图1. 我最爱的炮兵](/document/assert/img.jpg "Title")

![图2. 我的头像](https://sfault-avatar.b0.upaiyun.com/267/966/2679662993-581186b9d2f8a_big64 "Title")

{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}

{% img [box-model] http://weex.apache.org/cn/references/images/css-boxmodel.png 377 340 weex 盒模型 %}
```
效果：
![图1. 我最爱的炮兵](/document/assert/img.jpg "Title")

![图2. 我的头像](https://sfault-avatar.b0.upaiyun.com/267/966/2679662993-581186b9d2f8a_big64 "Title")

注：效果不显示
{% img [box-model] http://weex.apache.org/cn/references/images/css-boxmodel.png 377 340 weex 盒模型 %}


### 8. 代码

```
多行代码块使用三个`
单行代码使用一个`
console.log('hello world!')
```

### 9. 标题

```
方法1: - 和 = (任何数量等效)
一级标题
===
二级标题
---

方法2: #
# 一级 H1
## 二级 H2
### 三级 H3
#### 四级 H4
##### 五级 H5
###### 六级 H6
```
效果：
方法1: - 和 =
一级标题
===
二级标题
---

方法2: #
# 一级
## 二级
### 三级
#### 四级
##### 五级
###### 六级



### 10. jsfiddle

```
{% jsfiddle shorttag [tabs] [skin] [width] [height] %}

{% jsfiddle stardew/ffnm6Lsd/1/ %}  点击左上角fiddles
```

注：效果不显示
{% jsfiddle stardew/ffnm6Lsd/1/ %}



### 11. iframe


```
{% iframe url [width] [height] %}

{% iframe https://www.baidu.com/ 500 300 %}
```

注：效果不显示
{% iframe https://www.baidu.com/ 500 300 %}


### 12. 表格

```
左左中右对齐


dog | bird | cat
--- | ---- | ---
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

dog | bird | cat
:---- | :---- | :----
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

dog | bird | cat
:----: | :----: | :----:
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

dog | bird | cat
----: | ----: | ----:
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

```

dog | bird | cat
--- | ---- | ---
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

dog | bird | cat
:---- | :---- | :----
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

dog | bird | cat
:----: | :----: | :----:
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz

dog | bird | cat
----: | ----: | ----:
foo | foo  | foo
bar | bar  | bar
baz | baz  | baz



### 13. 原生代码

```
{% raw %}
content
{% endraw %}

或者直接
content

<span class="color-box" style="background:#FF00FF;color:#FF00FF"> yy </span> #FF00FF
```

注：效果不显示
<span class="color-box" style="background:#FF00FF;color:#FF00FF"> yy </span> #FF00FF

### 14. 转义

符号 | 转义
:----|:----
&#33; | `&#33;`
&#34; | `&#34;` 或 `&quot;`
&#35; | `&#35;`
&#36; | `&#36;`
&#37; | `&#37;`
&#38; | `&#38;` 或 `&amp;`
&#39; | `&#39;`
&#40; | `&#40;`
&#41; | `&#41;`
&#42; | `&#42;`
&#43; | `&#43;`
&#60; | `&#60;` 或 `&lt;`
&#61; | `&#61;`
&#62; | `&#62;` 或 `&gt;`
&#63; | `&#63;`
&#64; | `&#64;`
&#91; | `&#91;`
&#92; | `&#92;`
&#93; | `&#93;`
&#123; | `&#123;`
&#124; | `&#124;`
&#125; | `&#125;`

##### [转自] [hexo+css创建自己的blog（语法手册）](https://segmentfault.com/a/1190000011021195)