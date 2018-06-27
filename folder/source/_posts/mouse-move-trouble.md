---
title: mouse-move-trouble
date: 2015/07/29 13:03
tags: others
---

## mouseover、mouseout防止多次触发

今天做一个信息提示功能时，发现用mouseover展示提示信息，mouseout收起信息时，一直闪烁，开始以为层级关系出问题，修改许久未见成效，最后发现是因为内部元素在鼠标移上的时候会向它的父对...  

![](http://static.oschina.net/uploads/space/2015/0729/125346_K5Kp_255575.png)![](http://static.oschina.net/uploads/space/2015/0729/124752_Lwdz_255575.png)

    下面这段文字是摘抄的：  

        在用到mouseover和mouseout事件来作为事件触发的条件，但是如果我们用做触发的元素内部有其他的元素的时候当鼠标移上的时候会反复的触发mouseover和mouseout事件。因为内部元素在鼠标移上的时候会向它的父对象派发事件，所以外面元素相当于也触发了mouseover 事件。

        为了阻止mouseover和mouseout的反复触发，这里要用到event对象的一个属性relatedTarget，这个属性就是用来判断 mouseover和mouseout事件目标节点的相关节点的属性。简单的来说就是当触发mouseover事件时，relatedTarget属性代表的就是鼠标刚刚离开的那个节点，当触发mouseout事件时它代表的是鼠标移向的那个对象。由于MSIE不支持这个属性，不过它有代替的属性，分别是 fromElement和toElement。

    有了这个属性，我们就能够清楚的知道我们的鼠标是从哪个对象移过来，又是要移动到哪里去了。这样我们就能够通过判断这个相关联的对象是否在我们要触发事件的对象的内部，或者是不是就是这个对象本身。通过这个判断我们就能够合理的选择是否真的要触发事件。

    这里我们还用到了一个用于检查一个对象是否包含在另外一个对象中的方法，contains方法。MSIE和FireFox分别提供了检查的方法，这里封装了一个函数。

  

```
/*鼠标移入移出事件 防止多次触发*/
function contains(parentNode, childNode) {
    if (parentNode.contains) {
        return parentNode != childNode && parentNode.contains(childNode);
    } else {
        return !!(parentNode.compareDocumentPosition(childNode) & 16);
    }
}
function checkHover(e,target){
    if (getEvent(e).type=="mouseover")  {
        return !contains(target,getEvent(e).relatedTarget||getEvent(e).fromElement) && !((getEvent(e).relatedTarget||getEvent(e).fromElement)===target);
    } else {
        return !contains(target,getEvent(e).relatedTarget||getEvent(e).toElement) && !((getEvent(e).relatedTarget||getEvent(e).toElement)===target);
    }
}function getEvent(e){
    return e||window.event;
}
/*鼠标移入移出事件 防止多次触发*/
```

```
$(document).on("mouseover",".messages",function(e){
    if(checkHover(e,this)) {
        $(this).addClass("on");
        $(this).find(".m-txt").animate({right: "60px"}, 100);
    }
}).on("mouseout",".messages",function(e){
    if(checkHover(e,this)) {
        $(this).removeClass("on");
        $(this).find(".m-txt").animate({right: "-200px"}, 100);
    }
});
```

##### [转自] [mouseover、mouseout防止多次触发](https://my.oschina.net/luweiweiwei/blog/485108)