---
title: data-structure
date: 2016/12/09
tags: javascript
categories: 前端基础
---

# 数据结构基础 #

![](http://t1.aixinxi.net/o_1crp7bimtiq711qlla5jh1fq9a.png-w.jpg)

数据结构是相互之间存在一种或多种特定关系的数据元素的集合。  

数据元素相互之间的关系称为结构。  
 <!-- more -->
数据结构一共分四类：集合结构、线性结构、树型结构、图形结构。  

集合结构：具有某种特定性质的具体的或抽象的对象汇总成的集体。除了同属于一种类型外，别无其它关系。  

线性结构：元素之间存在一对一关系。  

特点：  

1. 存在唯一的一个被称作“第一个”的数据元素  

2. 存在唯一的一个被称作“最后一个”的数据元素  

3. 除第第一个以外，集合中的每个数据元素均只有一个前驱  

4. 除最后一个以外，集合中每个数据元素均只有一个后继  

常见类型有：  

1. 数组，链表，队列，栈。  

2. 它们之间在操作上有所区别。  

3. 例如：链表可在任意位置插入或删除元素，而队列在队尾插入元素，队头删除元素，栈只能在栈顶进行插入，删除操作。  

树形结构：元素之间存在一对多关系。  

常见类型有：  

1. 树

2. 有许多特例：二叉树、平衡二叉树、查找树等。  

    a. 满二叉树：深度为k且有2k-1个节点的二叉树  

![](http://t1.aixinxi.net/o_1crp7de6doh3ckac4q10kim04a.png-w.jpg)
![](http://t1.aixinxi.net/o_1crp7e3o52obl1f1sfk40b1dqla.png-w.jpg)

    b. 完全二叉树：深度为k，有n个节点的二叉树，当且仅当其每一个节点都与深度为k的满二叉树中编号从1至n的节点一一对应时，称之为完全二叉树。  

![](http://t1.aixinxi.net/o_1crp7euvq1nco1a7v1f0ou521ae9a.png-w.jpg)
![](http://t1.aixinxi.net/o_1crp7fkas1jk6pj5hs36792ura.png-w.jpg)

    c. huffman树：最优二叉树    

        i. 路径：从树中一个节点到另一个节点之间的分支构成这两个节点之间的路径  

        ii. 路径长度：路径上的分枝数目  

        iii. 树的带权路径长度为：WPL=w1l1+w2l2+...+wnln  

        iv. 假设有n个权值{w1,w2,…,wn}，试构造一颗有n个叶子节点的二叉树，每个叶子节点带权为wi，则其中带权路径长度WPL最小的二叉树称作最优二叉树（huffman树）  

        v. w=(5, 29, 7, 8, 14, 23, 3, 11), n=8, m=15, 构造huffman树。  

        教科书上结果：  

![](http://t1.aixinxi.net/o_1crp7gqlg1d3jdmjfkg16f0f0va.png-w.jpg)

WPL=3*4 + 5*4 + 7*4 + 8*4 + 11*3 + 14*3 + 23*2 + 29*2 = 271  

自己构造思路：从小到大排好序{3，5，7，8，11，14，23，29}，两两之和（红圈）与未构造数字（黑圈）比较，取小构造。  

![](http://t1.aixinxi.net/o_1crp7hghn1hcp2p71t241mpj1dvna.png-w.jpg)

WPL=3*5 + 5*5 + 7*4 + 8*3 + 11*3 + 14*3 + 23*2 +29*2 = 271
结论：huffman树构造结果不唯一。  

图形结构：元素之间存在多对多关系，图形结构中每个结点的前驱结点数和后续结点多个数可以任意(任意多个)。  

图的遍历包括深度优先遍历和广度优先遍历：  

![](http://t1.aixinxi.net/o_1crp7io0g1ra4v6413137h31ru6a.png-w.jpg)


深度优先遍历：v1—>v2—>v4—>v8—>v5—>v3—>v6—>v7  

![](http://t1.aixinxi.net/o_1crp7lgan1ubh13tu1b0h5tuhjma.png-w.jpg)


广度优先遍历：v1—>v2—>v3—>v4—>v5—>v6—>v7—>v8  

![](http://t1.aixinxi.net/o_1crp7m6dd1bso1egbtrg78k131qa.png-w.jpg)

最小生成树的问题：假设要在n个城市之间建立通信联络网，则连通n个城市只需要n-1条线路。这时。自然会考虑这样一个问题，如何在节省经费的前提下建立这个通信网。  

辅助表各参数说明：  

1. i行的1，2，3，4，5分别为（v2，v3，v4，v5，v6）  

2. k为最小边对应的i值  

3. 例如第三组3-3中的v6和2，表示（v1，v3，v6）与v4的最小边为v4---v6的权值2。  

![](http://t1.aixinxi.net/o_1crp7nos0ue71qle1jej1t60k0ia.png-w.jpg)
![](http://t1.aixinxi.net/o_1crp7op4398fdu4n9j1pp157oa.png-w.jpg)

哈希表：根据哈希函数H(key)和处理冲突的方法将一组关键字映射到一个有限的连续的地址集（区间）上，并以关键字在地址集中的“像”作为记录在表中的存储位置，这种表便称哈希表。  

构造哈希表：  

1. 直接定址法

2. 数字分析法

3. 平方取中法

4. 折叠法

5. 除留取余法

6. 随机数法

处理冲突的方法：  

1. 开放定址法

2. 再哈希法

3. 链地址法

4. 建立一个公共溢出区

常见数据结构  

1. 队列：队尾插入元素，队头删除元素。

2. 栈：栈顶进行插入、删除操作。

3. 堆：数组对象，可以被视为一棵完全二叉树结构。特点是父节点的值大于（小于）两个子节点的值（分别称为大顶堆和小顶堆）。

4. 链表：物理存储单元上非连续、非顺序的存储结构。插入删除有优势，查找弱势。

5. 数组：查找有优势，插入删除弱势，后面所有元素都需移动。

存储  

1. 栈区：由编译器自动分配释放，存放函数的参数值，局部变量的值等。其操作方式类似于数据结构中的栈。

2. 堆区：一般由程序员分配释放，若程序员不释放，程序结束时可能由OS回收。它与数据结构中的堆是两回事，分配方式倒是类似于链表。

##### [转自] [数据结构基础](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483751&idx=1&sn=7e36feb69c0f2a5049fb23b1c77624e8&chksm=eb02a111dc752807118a7db38335be7efe667a88c9e6a16fec2b8a40b76efe0d2dcbbba7a263&scene=0&key=aa3a7cd9173eb9043a79b0edce43c5ec046454ba47464922369ebba4e583a0cea87885455878181c435dcd5f116a111177f2d2b3bee812558f528e290c8e0da6def301d0405c05fecf148e78fb829e29&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)