---
title: extend
date: 2016/12/9
tags: javascript
categories: 前端基础
---

大多数面向对象语言都支持两种继承方式：接口继承和实现继承。  

而ECMAScript中无法实现接口继承，只支持实现继承。  

其实现继承主要依靠原型链来实现。  
 <!-- more -->
##### 1. 原型链

基本思想：利用原型让一个引用类型继承另外一个引用类型的属性和方法。  
```
function superObj () {

	this.name = 'lujiang';

}

superObj.prototype.getSuperVal = function () {

	return 'super ' + this.name;

}

function subObj () {

	this.name = 'weilu';

}

subObj.prototype = new superObj();

subObj.prototype.getSubVal = function () {

	return 'sub ' + this.name;

}

var obj = new subObj();

console.log(obj.getSuperVal());// super weilu
```

##### 2. 借用构造函数

基本思想：在子类型构造函数的内部调用父类构造函数，通过call()和apply()方法在新创建的对象上执行构造函数。  
```
function superObj () {

	this.colors = ['yellow', 'green', 'blue'];

}

function subObj () {

	superObj.call(this);

}

var obj = new subObj();

obj.colors.push('purple');

console.log(obj.colors);// ["yellow", "green", "blue", "purple"]

var objj = new subObj();

console.log(objj.colors);// ["yellow", "green", "blue"]
```

##### 3. 组合继承

基本思想：将原型连和借用构造函数组合起来，发挥两者之长。  
```
function superObj (name) {

	this.name = name;

	this.colors = ["yellow", "green", "blue"];

}

superObj.prototype.getName = function () {

	console.log('name = ' + this.name);

}

function subObj (name, age) {

	superObj.call(this, name);

	this.age = age;

}

subObj.prototype = new superObj();

subObj.prototype.constructor = subObj;

subObj.prototype.getAge = function () {

	console.log('age = ' + this.age);

}

var obj = new subObj('lujiang', 25);

obj.colors.push('purple');

console.log(obj.colors);// ["yellow", "green", "blue", "purple"]

obj.getName();// name = lujiang

obj.getAge();// age = 25

var objj = new subObj('weilu', 25.5);

console.log(objj.colors);// ["yellow", "green", "blue"]

objj.getName();// name = weilu

objj.getAge();// age = 25.5
```

##### 4. 原型式继承

基本思想：借助原型基于已有对象创建新对象。  
```
function object (o) {

	function F () {}

	F.prototype = o;

	return new F();

}

var Person = {

	name: 'lujiang',

	colors: ['yellow', 'green', 'blue']

}

var secondPerson = object(Person);

secondPerson.name = 'weilu';

secondPerson.colors.push('purple');

var thirdPerson = object(Person);

thirdPerson.name = 'dew';

thirdPerson.colors.push('golden');

console.log(Person, secondPerson, thirdPerson);

// Object {name: "lujiang", colors: Array[5]}

// F {name: "weilu"}

// 如上，展示全：Fname: "weilu"__proto__: Objectcolors: Array[5]name: "lujiang"__proto__: Object

// F {name: "dew"}

// 如上，展示全：Fname: "dew"__proto__: Objectcolors: Array[5]name: "lujiang"__proto__: Object



// ECMAScript5  Object.create = 上述 function Object

// Object.create() 方法创建一个拥有指定原型和若干个指定属性的对象。

var Person = {

	name: 'lujiang',

	colors: ['yellow', 'green', 'blue']

}

var secondPerson = Object.create(Person);

secondPerson.name = 'weilu';

secondPerson.colors.push('purple');

var thirdPerson = Object.create(Person);

thirdPerson.name = 'dew';

thirdPerson.colors.push('golden');

console.log(Person.colors, secondPerson.colors, thirdPerson.colors);

// ["yellow", "green", "blue", "purple", "golden"]

// ["yellow", "green", "blue", "purple", "golden"]

// ["yellow", "green", "blue", "purple", "golden"]

console.log(secondPerson.__proto__ === thirdPerson.__proto__);// true

console.log(secondPerson.__proto__ === Person);// true
```

##### 5. 寄生式继承

基本思想：创建一个仅用于封装继承过程的函数。  
```
function extend (orl) {

	var F = Object(orl);

	F.getName = function () {

		console.log('lujiang');

	}

	return F;

}

var Person = {

	name: 'lujiang',

	colors: ['yellow', 'green', 'blue']

}

var secondPerson = extend(Person);

secondPerson.getName(); // lujiang
```

##### 6. 寄生组合式继承

基本思想：通过借用构造函数(2)来继承*属性*，通过原型链(1)与与原型式继承(4)形式来继承*方法*。  
```
function extend (subObj, superObj) {

	var P = Object(superObj.prototype);// 通过原型链(1)与与原型式继承(4)形式来继承*方法*

	P.constructor = subObj;

	subObj.prototype = P;

}

function superObj (name) {

	this.name = name;

	this.colors = ['yellow', 'green', 'blue'];

}

superObj.prototype.getName = function () {

	console.log('name = ' + this.name);

}

function subObj (name, age) {

	superObj.call(this, name);// 通过借用构造函数(2)来继承*属性*

	this.age = age;

}

extend(subObj, superObj);

subObj.prototype.getAge = function () {

	console.log('age = ' + this.age);

}

var obj = new subObj('lujiang');

obj.colors.push('purple');

console.log(obj.colors);// ["yellow", "green", "blue", "purple"]

obj.getName();// name = lujiang
```


##### [转自] [javascript的实现继承](https://mp.weixin.qq.com/s?__biz=MzI3NTQ5NTE5Mw==&mid=2247483754&idx=1&sn=7ed2b3a5ae099b35e5f58bf424d26b65&chksm=eb02a11cdc75280aa0b6adfe31845639854d52bbd7345e113ecc1014a472a11c54b045688583&scene=0&key=aa3a7cd9173eb9048482ff51598554328984781eb73f34e7f10a49ea0da4ff2f46f2e2ae34d5fb7b9738ca250b9381ce27ce1943f532e4bbb5079777eea4c04bd535ff71a4b907405a55551a5f12265a&ascene=0&uin=NzgyNzAwMTAx&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.12.4+build&version=12020610&nettype=WIFI&lang=zh_CN&fontScale=100&pass_ticket=3r5tdwajo%2Bn%2FJyql48TdVB%2FIyWmFLBAbbtRIhDbY8dpbaiMNp6ziZZAl21WufchK)