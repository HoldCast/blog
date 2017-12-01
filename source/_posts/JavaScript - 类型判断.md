title: JavaScript - 对象类型判断
tags:
    - javascript
    - 类型判断
---
- typeof 判断
- instanceof 运算符
- constructor 属性
- Object.prototype.toString() 判断

<!-- more -->
### 1.typeof 判断
在区别对象和原始类型的时候可使用这种判断方法,其返回值有:"number"，"string"，"boolean"，"object"，"function"，"undefined"（可用于判断变量是否存在）.
但typeof有局限，其对于null、{}、[]、Date、RegExp等类型返回的都是"object"。如：
typeof {}; // object
typeof []; // object
typeof null; // object
typeof new Date(); // object;

### 2.instanceof 运算符
instanceof 运算符要求其左边的运算数是一个对象，右边的运算数是对象类的名字或构造函数。如果 object 是 class 或构造函数的实例，则 instanceof 运算符返回 true。
如果 object 不是指定类或函数的实例，或者 object 为 null，则返回 false。如：
[] instanceof Array; // true
[] instanceof Object; // true
[] instanceof RegExp; // false
new Date instanceof Date; // true
 *可以用instanceof运算符来判断对象是否为数组类型.*

### 3.constructor 属性
JavaScript中，每个对象都有一个constructor属性，它引用了初始化该对象的构造函数，常用于判断未知对象的类型。
通过typeof运算符来判断它是原始的值还是对象。如果是对象，就可以使用constructor属性来判断其类型。所以判断数组的函数也可以这样写：
function isArray(arr){
  return typeof arr == "object" && arr.constructor == Array;
}

### 4.Object.prototype.toString() 判断
** \*这种方法可以准确判断各种数据类型\* **
Object.prototype.toString.call([]); // "[object Array]"
Object.prototype.toString.call(/reg/ig); // "[object RegExp]"
Object.prototype.toString.call(999); // "[object Number]"
用于检测各种对象类型：
```
var is ={
  types : ["Array", "Boolean", "Date", "Number", "Object", "RegExp", "String", "Window", "HTMLDocument"]
};
for(var i = 0, c; c = is.types[i ++ ]; ){
  is[c] = (function(type){
    return function(obj){
      return Object.prototype.toString.call(obj) == "[object " + type + "]";
    }
  )(c);
}
alert(is.Array([])); // true
alert(is.Date(new Date)); // true
alert(is.RegExp(/reg/ig)); // true
//...
```