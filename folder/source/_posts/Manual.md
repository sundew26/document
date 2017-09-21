---
title: Manual
date: 2017-08-24 15:26:08
updated: 2017-08-24 15:26:08
tags:
---

语法使用手册
---

1. 列表:
---
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
效果:
1. 第一点
2. 第二点
3. 第三点
* 星号列表
+ 加号列表
- 减号列表

2. 块注释
---
```
> 区块引用
下一行

或者:
{% blockquote %}
普通的引用
下一行
{% endblockquote %}

嵌套引用
> 一层
>> 两层
```
效果:
> 区块引用
  下一行

{% blockquote %}
普通的引用
下一行
{% endblockquote %}

> 一层
>> 两层
>

3. 分割线
---
```
虚线:
***
或者(实线)
---
```
效果:

***
虚线

---
实线


4. 链接
---
```
[这是一个绝对路径的链接](https://hexo.io/zh-cn/docs/writing.html)
[这是一个相对路径的链接](/2017/08/07/hello-world/)
```
[这是一个绝对路径的链接](https://hexo.io/zh-cn/docs/writing.html)
[这是一个相对路径的链接](/2017/08/07/hello-world/)

5. 加粗
---
```
**双星加粗**
__双下划线加粗__
```
**双星加粗**
__双下划线加粗__

6. 斜体
---

```
*星号斜体*
_下划线斜体_
```
*星号斜体*
_下划线斜体_

7. 删除线
```
~~删除线~~
```
~~删除线~~

8. 图片
---
```
![图1. 我最爱的炮兵](/assert/img.jpg "Title")

{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}

{% img [box-model] http://weex.apache.org/cn/references/images/css-boxmodel.png 377 340 weex 盒模型 %}
```
![图1. 我最爱的炮兵](/assert/img.jpg "Title")

{% img [box-model] http://weex.apache.org/cn/references/images/css-boxmodel.png 377 340 weex 盒模型 %}

9. 代码
---
![](/assert/code.png "Title")
```
多行代码块使用三个`
单行代码使用一个`
console.log('hello world!')
```

10. 标题
---
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

11. jsfiddle
===
```
{% jsfiddle shorttag [tabs] [skin] [width] [height] %}

{% jsfiddle stardew/ffnm6Lsd/1/ %}  点击左上角fiddles
```
{% jsfiddle stardew/ffnm6Lsd/1/ %}

12. iframe
===
```
{% iframe url [width] [height] %}

{% iframe https://www.baidu.com/ 500 300 %}
```

{% iframe https://www.baidu.com/ 500 300 %}

13. link
===
```
{% link text url [external] [title] %}

你好,我是{% link 百度 https://www.baidu.com/ 搜索  度娘 %}.
```

##### 你好,我是{% link 百度 https://www.baidu.com/ 搜索  度娘 %}.

14. 表格
===

```
左中右对齐


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

15. 原生代码
===

```
{% raw %}
content
{% endraw %}

或者直接
content

<span class="color-box" style="background:#FF00FF;color:#FF00FF"> yy </span> #FF00FF
```

<span class="color-box" style="background:#FF00FF;color:#FF00FF"> yy </span> #FF00FF

16. 转义
===

符号 | 转义
:----:|:----:
! | `&#33;`
” | `&#34;` 或 `&quot;`
# | `&#35;`
$ | `&#36;`
% | `&#37;`
& | `&#38;` 或 `&amp;`
‘ | `&#39;`
( | `&#40;`
) | `&#41;`
* | `&#42;`
+ | `&#43;`
< | `&#60;` 或 `&lt;`
= | `&#61;`
> | `&#62;` 或 `&gt;`
? | `&#63;`
@ | `&#64;`
[ | `&#91;`
\ | `&#92;`
] | `&#93;`
{ | `&#123;`
&#124; | `&#124;`(竖线)
} | `&#125;`
