title: jQuery常用方法
date: 2017/1/1 23:54
categories:
- JavaScript
tags:
- jQuery
---
jQuery是一个快速、简洁的JavaScript框架，是继Prototype之后又一个优秀的JavaScript代码库（JavaScript框架）。jQuery设计的宗旨是“write Less，Do More”，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML文档操作、事件处理、动画设计和Ajax交互。jQuery的核心特性可以总结为:具有独特的链式语法和短小清晰的多功能接口；具有高效灵活的css选择器，并且可对CSS选择器进行扩展；拥有便捷的插件扩展机制和丰富的插件。本文总结了jQuery常用的方法，辅以代码说明。
<!--more-->

----
### $.trim
$.trim方法用于移除字符串头部和尾部多余的空格。
```javascript
$.trim('  Hello  '); // Hello
```

----
### $.contains
$.contains方法返回一个布尔值，表示某个DOM元素（第二个参数）是否为另一个DOM元素（第一个参数）的下级元素。
```javascript
$.contains(document.documentElement, document.body);  // true
$.contains(document.body, document.documentElement);  // false
```

----
### $.each
$.each方法用于遍历数组和对象，然后返回原始对象。它接受两个参数，分别是数据集合和回调函数。
```javascript
$.each([ 52, 97 ], function( index, value ) {
  console.log( index + ": " + value );
});
// 0: 52 
// 1: 97 
var obj = {
  p1: "hello",
  p2: "world"
};
$.each( obj, function( key, value ) {
  console.log( key + ": " + value );
});
// p1: hello
// p2: world
```
需要注意的，jQuery对象实例也有一个each方法（$.fn.each），两者的作用差不多。

----
### $.map
$.map方法也是用来遍历数组和对象，但是会返回一个新对象。
```javascript
var a = ["a", "b", "c", "d", "e"];
a = $.map(a, function (n, i){
  return (n.toUpperCase() + i);
});
// ["A0", "B1", "C2", "D3", "E4"]
```

----
### $.inArray
$.inArray方法返回一个值在数组中的位置（从0开始）。如果该值不在数组中，则返回-1。
```javascript
var a = [1,2,3,4];
$.inArray(4,a); // 3
```

----
### $.extend
$.extend方法用于将多个对象合并进第一个对象。
```javascript
var o1 = {p1:'a',p2:'b'};
var o2 = {p1:'c'};
$.extend(o1,o2);
o1.p1; // "c"
```
$.extend的另一种用法是生成一个新对象，用来继承原有对象。这时，它的第一个参数应该是一个空对象。
```javascript
var o1 = {p1:'a',p2:'b'};
var o2 = {p1:'c'};
var o = $.extend({},o1,o2);
o; // Object {p1: "c", p2: "b"}
```
默认情况下，extend方法生成的对象是“浅拷贝”，也就是说，如果某个属性是对象或数组，那么只会生成指向这个对象或数组的指针，而不会复制值。如果想要“深拷贝”，可以在extend方法的第一个参数传入布尔值true。
```javascript
var o1 = {p1:['a','b']};
var o2 = $.extend({},o1);
var o3 = $.extend(true,{},o1);
o1.p1[0]='c';
o2.p1; // ["c", "b"]
o3.p1; // ["a", "b"] 
```
上面代码中，o2是浅拷贝，o3是深拷贝。结果，改变原始数组的属性，o2会跟着一起变，而o3不会。

也就是说浅拷贝类似双向绑定。

----
### $.proxy
$.proxy方法类似于ECMAScript 5的bind方法，可以绑定函数的上下文（也就是this对象）和参数，返回一个新函数。
jQuery.proxy()的主要用处是为回调函数绑定上下文对象。
```javascript
var o = {
    type: "object",
    test: function(event) {
        console.log(this.type);
    }
};
$("#button").on("click", o.test); // 无输出
 $("#button").on("click", $.proxy(o.test, o)); // object
```
上面的代码中，第一个回调函数没有绑定上下文，所以结果为空，没有任何输出；第二个回调函数将上下文绑定为对象o，结果就为object。
这个例子的另一种等价的写法是：
```javascript
$("#button").on( "click", $.proxy(o, test)); 
```
上面代码的$.proxy(o, test)的意思是，将o的方法test与o绑定。
这个例子表明，proxy方法的写法主要有两种。
```javascript
jQuery.proxy(function, context);
// or
jQuery.proxy(context, name);
```
第一种写法是为函数（function）指定上下文对象（context），第二种写法是指定上下文对象（context）和它的某个方法名（name）。
再看一个例子。正常情况下，下面代码中的this对象指向发生click事件的DOM对象。
```javascript
$('#myElement').click(function() {
    $(this).addClass('aNewClass');
});
```
如果我们想让回调函数延迟运行，使用setTimeout方法，代码就会出错，因为setTimeout使得回调函数在全局环境运行，this将指向全局对象。
```javascript
$('#myElement').click(function() {
    setTimeout(function() {
        $(this).addClass('aNewClass');
    }, 1000);
});
```
上面代码中的this，将指向全局对象window，导致出错。这时，就可以用proxy方法，将this对象绑定到myElement对象。
```javascript
$('#myElement').click(function() {
    setTimeout($.proxy(function() {
        $(this).addClass('aNewClass'); 
    }, this), 1000);
});
```

----
### $.data
$.data方法可以用来在DOM节点上储存数据。
```javascript
// 存入数据
$.data(document.body, "foo", 52 );
// 读取数据
$.data(document.body, "foo");
// 读取所有数据
$.data(document.body);
```
上面代码在网页元素body上储存了一个键值对，键名为“foo”，键值为52。
$.removeData方法用于移除所存储的数据。
```javascript
$.data(div, "test1", "VALUE-1");
$.removeData(div, "test1");
```

----
### $.parseHTML  
$.parseHTML方法用于将字符串解析为DOM对象。
```javascript
var html = $.parseHTML("hello, <b>my name is</b> jQuery.");
```

----
### $.parseJSON
$.parseJSON方法用于将JSON字符串解析为JavaScript对象，作用与原生的JSON.parse()类似。但是，jQuery没有提供类似JSON.stringify()的方法，即不提供将JavaScript对象转为JSON对象的方法。
```javascript
var obj = $.parseJSON('{"name": "John"}');
```

----
### $.parseXML
$.parseXML方法用于将字符串解析为XML对象。
```javascript
var xml = "<rss version='2.0'><channel><title>RSS Title</title></channel></rss>";
var xmlDoc = $.parseXML(xml);
```

----
### $.makeArray
$.makeArray方法将一个类似数组的对象，转化为真正的数组。
```javascript
var a = $.makeArray(document.getElementsByTagName("div"));
```

----
### $.merge
$.merge方法用于将一个数组（第二个参数）合并到另一个数组（第一个参数）之中。
````javascript
var a1 = [0,1,2];
var a2 = [2,3,4];
$.merge(a1, a2);
a1;
// [0, 1, 2, 2, 3, 4]
````

----
### $.now
$.now方法返回当前时间距离1970年1月1日00:00:00 UTC对应的毫秒数，等同于(new Date).getTime()，即时间戳。
```javascript
$.now();
//1480860477 2016年12月04日 22:07:57
```

----
### 判断数据类型的方法
jQuery提供一系列工具方法，用来判断数据类型，以弥补JavaScript原生的**typeof**运算符的不足。以下方法对参数进行判断，返回一个布尔值。
**jQuery.isArray()**：是否为数组。
**jQuery.isEmptyObject()**：是否为空对象（不含可枚举的属性）。
**jQuery.isFunction()**：是否为函数。
**jQuery.isNumeric()**：是否为数组。
**jQuery.isPlainObject()**：是否为使用“{}”或“new Object”生成的对象，而不是浏览器原生提供的对象。
**jQuery.isWindow()**：是否为window对象。
**jQuery.isXMLDoc()**：判断一个DOM节点是否处于XML文档之中。
```javascript
$.isEmptyObject({}); // true
$.isPlainObject(document.location); // false
$.isWindow(window); // true
$.isXMLDoc(document.body); // false
```
除了上面这些方法以外，还有一个**$.type**方法，可以返回一个变量的数据类型。它的实质是用**Object.prototype.toString**方法读取对象内部的[[Class]]属性。
```javascript
$.type(/test/); // "regexp"
```
