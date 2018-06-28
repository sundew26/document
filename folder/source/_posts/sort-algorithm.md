---
title: sort-algorithm
date: 2011/01/01
tags: javascript
---

![](https://mmbiz.qpic.cn/mmbiz_jpg/0vF1DtfHb3EIQuBbqgJUpWpwoCzwvUsyBBLzwRs3xzJiczn5iaYxlETqInbX1T8YFF8EGl1PyCg9Dr4MoVyQTKrw/0?wx_fmt=jpeg)

不稳定排序（快选堆希）  

简单排序中直接插入最好，快速排序最快，当文件为正序时，直接插入和冒泡均最佳。

影响因素：  

①待排序的记录数目n；  

②记录的大小(规模)；  

③关键字的结构及其初始状态；  

④对稳定性的要求；  

⑤语言工具的条件；  

⑥存储结构；  

⑦时间和辅助空间复杂度等。  

不同条件下，排序方法的选择：  

  (1)若n较小(如n≤50)，可采用直接插入或直接选择排序。  

    当记录规模较小时，直接插入排序较好；否则因为直接选择移动的记录数少于直接插人，应选直接选择排序为宜。  

  (2)若文件初始状态基本有序(指正序)，则应选用直接插人、冒泡或随机的快速排序为宜；  

  (3)若n较大，则应采用时间复杂度为O(nlgn)的排序方法：快速排序、堆排序或归并排序。  

    快速排序是目前基于比较的内部排序中被认为是最好的方法，当待排序的关键字是随机分布时，快速排序的平均时间最短；  

    堆排序所需的辅助空间少于快速排序，并且不会出现快速排序可能出现的最坏情况。这两种排序都是不稳定的。  

    若要求排序稳定，则可选用归并排序。但本章介绍的从单个记录起进行两两归并的  排序算法并不值得提倡，通常可以将它和直接插入排序结合在一起使用。先利用直接插入排序求得较长的有序子文件，然后再两两归并之。因为直接插入排序是稳定 的，所以改进后的归并排序仍是稳定的。  


### 一.冒泡排序

描述：两层循环，依次比较两个相邻的元素，如果反序则调换位置。  

时间复杂度：时间：最好o(n), 最差o(n*(n-1))  

空间复杂度：o(1)  

```
function bubbleSort (arr) {

  for (var i = 0, len = arr.length; i < len; i++) {

    for (var j = i + 1; j < len; j++) {

      if(arr[i] > arr[j]) {

        var temp = arr[i];

        arr[i] = arr[j];

        arr[j] = temp;

      }

    }

    console.log(arr);

  }

  return arr;

}



var arr = [20, 1, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30];

bubbleSort(arr);



/*

[1, 20, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30]

[1, 2, 20, 60, 4, 6, 7, 8, 9, 8, 5, 3, 3, 30]

[1, 2, 3, 60, 20, 6, 7, 8, 9, 8, 5, 4, 3, 30]

[1, 2, 3, 3, 60, 20, 7, 8, 9, 8, 6, 5, 4, 30]

[1, 2, 3, 3, 4, 60, 20, 8, 9, 8, 7, 6, 5, 30]

[1, 2, 3, 3, 4, 5, 60, 20, 9, 8, 8, 7, 6, 30]

[1, 2, 3, 3, 4, 5, 6, 60, 20, 9, 8, 8, 7, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 60, 20, 9, 8, 8, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 60, 20, 9, 8, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 60, 20, 9, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 60, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

*/
```

### 二.快速排序

描述：选取第一个为基数，大于这个基数的存入一个数组，小于这个基数的存入一个数组，最后拼接递归。  

时间复杂度：时间：最好o(nlgn) , 最差o(n*n)  

空间复杂度：o(lgn)  

```
function quickSort (arr) {

  var len = arr.length;

  if (len <= 1) {

    return arr;

  } else {

    var base = [arr[0]];

    var small = [];

    var big = [];

    for (var i=1; i<len; i++) {

      if(arr[i] < base) {

        small.push(arr[i]);

      } else if(arr[i] >= base) {

        big.push(arr[i]);

      }

    }

    console.log(small.concat(base.concat(big)));

    return quickSort(small).concat(base.concat(quickSort(big)));

  }

}



var arr = [20, 1, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30];

quickSort(arr);



/*

[1, 3, 4, 6, 7, 8, 9, 8, 5, 3, 2, 20, 60, 30]

[1, 3, 4, 6, 7, 8, 9, 8, 5, 3, 2]

[2, 3, 4, 6, 7, 8, 9, 8, 5, 3]

[3, 4, 6, 7, 8, 9, 8, 5]

[5, 6, 7, 8, 9, 8]

[7, 8, 9, 8]

[8, 9, 8]

[8, 9]

[30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

*/
```

### 三.选择排序

描述： 每次从数组里选出一个最小的元素，标出位置，和第一个比较，如果反序，则调换位置。  

时间复杂度：时间：最好o(n*n) , 最差o(n*n)  

空间复杂度：o(1)  

```
function selectSort (arr) {

  var len = arr.length;

  for (var i = 0; i < len; i++) {

    var min = arr[i];

    var minIdx = i;

    for (var j = i + 1; j < len; j++) {

      if (min > arr[j]) {

        min = arr[j];

        minIdx = j

      }

    }

    if (i !== minIdx) {

      var temp = arr[i];

      arr[i] = min;

      arr[minIdx] = temp;

    }

    console.log(arr);

  }

  return arr;

}



var arr = [20, 1, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30];

selectSort(arr);



/*

[1, 20, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30]

[1, 2, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 20, 30]

[1, 2, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 20, 30]

[1, 2, 3, 3, 4, 6, 7, 8, 9, 8, 5, 60, 20, 30]

[1, 2, 3, 3, 4, 6, 7, 8, 9, 8, 5, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 7, 8, 9, 8, 6, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 6, 8, 9, 8, 7, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 9, 8, 8, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 9, 8, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 60, 20, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 60, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

*/
```

#### 四.插入排序（直接插入排序）

描述：按下标顺序，往一个有序数组中插入，位置为比当前数据小的元素之后  

时间复杂度：时间：最好 o(n), 最差o(n*n)  

空间复杂度：o(1)  

```
function insertSort (arr) {

  var len = arr.length;

  for (var i = 0; i < len - 1; i++) {

    var idx = i + 1;

    var insert = arr[idx];

    for (var j = i ; j >= 0; j--) {

      if (insert < arr[j]) {

        arr[j+1] = arr[j];

        idx = j

      }

    }

    arr[idx] = insert;

    console.log(arr);

  }

  return arr;

}



var arr = [20, 1, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30];

insertSort(arr);



/*

[1, 20, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30]

[1, 3, 20, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30]

[1, 3, 20, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30]

[1, 3, 4, 20, 60, 6, 7, 8, 9, 8, 5, 3, 2, 30]

[1, 3, 4, 6, 20, 60, 7, 8, 9, 8, 5, 3, 2, 30]

[1, 3, 4, 6, 7, 20, 60, 8, 9, 8, 5, 3, 2, 30]

[1, 3, 4, 6, 7, 8, 20, 60, 9, 8, 5, 3, 2, 30]

[1, 3, 4, 6, 7, 8, 9, 20, 60, 8, 5, 3, 2, 30]

[1, 3, 4, 6, 7, 8, 8, 9, 20, 60, 5, 3, 2, 30]

[1, 3, 4, 5, 6, 7, 8, 8, 9, 20, 60, 3, 2, 30]

[1, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 60, 2, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 60, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

*/
```

#### 五.希尔排序（插入排序的一种）

描述：按gap步依次比较，gap按length/2依次减小  

时间复杂度：时间：最好 , 最差  

空间复杂度：o(1)  

```
function shellSort (array) {

  var length = array.length;

  var gap = Math.round(length / 2);

  while (gap > 0) {

    for (var i = gap; i < length; i++) {

      var insert = array[i];

      var index = i;

      for (var j = i; j >= 0; j -= gap) {

        if (insert < array[j]) {

          array[j+gap] = array[j];

          index = j;

        }

      }

      array[index] = insert;

    }

    console.log(array);

    gap = Math.round(gap/2 - 0.1);

  }

  return array;

}



var arr = [20, 1, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30];

shellSort(arr);



/*

[8, 1, 3, 5, 3, 2, 7, 20, 9, 8, 60, 4, 6, 30]

[5, 1, 2, 6, 3, 3, 7, 20, 4, 8, 30, 9, 8, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

*/
```

#### 六.归并排序

描述：先将每个子序列排序，再将已有序列的子序列合并。

时间复杂度：时间：最好：n(lgn) , 最差n(lng)

空间复杂度：o(n)

```
function mergeSort (array) {

  var length = array.length;

  if (length <= 1) {

    return array;

  } else {

    var num = Math.ceil(length / 2);

    var left = mergeSort(array.slice(0, num));

    var right = mergeSort(array.slice(num, length));

    return merge(left, right);

  }

}



function merge (left, right) {

  console.log(left);

  console.log(right);

  var a = new Array();

  while (left.length > 0 && right.length > 0) {

    if (left[0] <= right[0]) {

      var temp = left.shift();

      a.push(temp);

    } else {

      var temp = right.shift();

      a.push(temp);

    }

  }

  if (left.length > 0) {

    a = a.concat(left);

  }

  if (right.length > 0) {

    a = a.concat(right);

  }

  console.log(a);

  console.log("-----------------------------");

  return a;

}



var arr = [20, 1, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30];

mergeSort(arr);



/*

[1]

[1, 20]

-----------------------------

[3]

[60]

[3, 60]

-----------------------------

[1, 20]

[3, 60]

[1, 3, 20, 60]

-----------------------------

[4]

[6]

[4, 6]

-----------------------------

[4, 6]

[7]

[4, 6, 7]

-----------------------------

[1, 3, 20, 60]

[4, 6, 7]

[1, 3, 4, 6, 7, 20, 60]

-----------------------------

[8]

[9]

[8, 9]

-----------------------------

[8]

[5]

[5, 8]

-----------------------------

[8, 9]

[5, 8]

[5, 8, 8, 9]

-----------------------------

[3]

[2]

[2, 3]

-----------------------------

[2, 3]

[30]

[2, 3, 30]

-----------------------------

[5, 8, 8, 9]

[2, 3, 30]

[2, 3, 5, 8, 8, 9, 30]

-----------------------------

[1, 3, 4, 6, 7, 20, 60]

[2, 3, 5, 8, 8, 9, 30]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

-----------------------------

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

*/
```

#### 七、堆排序（选择排序的一种）

描述：先要建一棵二叉树，然后按最大堆或最小堆调节每个节点。  

时间复杂度：时间：最好o(nlgn) , 最差o(nlgn)  

空间复杂度：o()  

```
Array.prototype.buildMaxHeap = function () {

  for (var i = Math.floor(this.length / 2) - 1; i >= 0; i--) {

    this.heapAdjust(i, this.length);

  }

};



Array.prototype.swap = function (i, j) {

  var tmp = this[i];

  this[i] = this[j];

  this[j] = tmp;

};



Array.prototype.heapSort = function () {

  this.buildMaxHeap();

  for (var i = this.length - 1; i > 0; i--) {

    this.swap(0, i);

    this.heapAdjust(0, i);

    console.log(this);

  }

  return this;

};



Array.prototype.heapAdjust = function (i,j) {

  var largest = i;

  var left = 2 * i + 1;

  var right = 2 * i + 2;

  if (left < j && this[largest] < this[left]) {

    largest = left;

  }

  if (right < j && this[largest] < this[right]) {

    largest = right;

  }

  if (largest != i) {

    this.swap(i, largest);

    this.heapAdjust(largest, j);

  }

};



var a = new Array();

[].push.apply(a, [20, 1, 3, 60, 4, 6, 7, 8, 9, 8, 5, 3, 2, 30]);

a.heapSort();



/*

[30, 20, 7, 9, 8, 6, 3, 8, 1, 4, 5, 3, 2, 60]

[20, 9, 7, 8, 8, 6, 3, 2, 1, 4, 5, 3, 30, 60]

[9, 8, 7, 3, 8, 6, 3, 2, 1, 4, 5, 20, 30, 60]

[8, 8, 7, 3, 5, 6, 3, 2, 1, 4, 9, 20, 30, 60]

[8, 5, 7, 3, 4, 6, 3, 2, 1, 8, 9, 20, 30, 60]

[7, 5, 6, 3, 4, 1, 3, 2, 8, 8, 9, 20, 30, 60]

[6, 5, 3, 3, 4, 1, 2, 7, 8, 8, 9, 20, 30, 60]

[5, 4, 3, 3, 2, 1, 6, 7, 8, 8, 9, 20, 30, 60]

[4, 3, 3, 1, 2, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[3, 2, 3, 1, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[3, 2, 1, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[2, 1, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

[1, 2, 3, 3, 4, 5, 6, 7, 8, 8, 9, 20, 30, 60]

*/
```

排序方法 | 最好时间 | 平均时间 | 最坏时间 | 辅助空间 | 稳定性 | 使用场景
--- | --- | --- | --- | --- | --- | ---
冒泡 | O(n) | O(n<sup>2</sup>) | O(n<sup>2</sup>) | O(1) | --- | 正序
快速 | O(nlgn) | O(nlgn) | O(n<sup>2</sup>) | O(lgn) | 不稳定 | 正序、n较大
选择 | O(n<sup>2</sup>) | O(n<sup>2</sup>) | O(n<sup>2</sup>) | O(1) | 不稳定 | n<=50(佳)
插入 | O(n) | O(n<sup>2</sup>) | O(n<sup>2</sup>) | O(1) | --- | n<=50、正序
希尔(插入) | O(n) | O(n<sup>1.25</sup>) | O(n<sup>2</sup>) | O(1) | 不稳定 | 正序
归并 | O(nlgn) | O(nlgn) | O(nlgn) | O(n) | --- | n较大
堆(树形选择) | O(nlgn) | O(nlgn) | O(nlgn) | O(1) | 不稳定 | n较大



##### [转自] [排序算法](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483756&idx=1&sn=75f5e46d7167e23442904496c1249e3f&chksm=eb02a11adc75280c941e832d2216c3cdc0eb2dcbf8f9987ea95c02acda75463d289c7361a543&mpshare=1&scene=1&srcid=0628eP2TJDVt4sUCjtQ9UHUu&key=5ab28f7f3e673bf14e8e3e03ddcf392ca3979b8e247708fc459e5db81c35a97d381d540e5b4486155e2943b2b68593274d290cb9132fa5615fec2f7a1687d49c3766eeb06e98149045c012f29c9d9cb9&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build(16E195)&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)