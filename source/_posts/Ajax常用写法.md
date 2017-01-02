title: Ajax常用写法
date: 2017/1/2 10:23
categories:
- JavaScript
tags:
- jQuery
- Ajax
---
AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的网页开发技术。AJAX 是一种用于创建快速动态网页的技术。通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。本文介绍了Ajax的常用写法，以及各个属性的解释说明，使之有一个大致的了解。
<!--more-->
### $.ajax
jQuery对象上面还定义了Ajax方法($.ajax())，用来处理Ajax操作。调用该方法后，浏览器就会向服务器发出一个HTTP请求。
$.ajax()的用法有多种，最常见的是提供一个对象参数。
```javascript
$.ajax({
  	async: true,
  	url: '/url/to/json',
  	type: 'GET',
  	data : { id : 123 },
  	dataType: 'json',
  	timeout: 30000,
  	success: successCallback,
  	error: errorCallback,
  	complete: completeCallback
});
function successCallback(json) {
    $('<h1/>').text(json.title).appendTo('body');
},
function errorCallback(xhr, status){
    console.log('出问题了！');
},
function completeCallback(xhr, status){
    console.log('Ajax请求已结束。');
}
```
上面代码的对象参数有多个属性，含义如下：
**async**：该项默认为true，如果设为false，则表示发出的是同步请求。
**cache**: 该项默认为true，如果设为false，则浏览器不缓存返回服务器返回的数据。注意，浏览器本身就不会缓存POST请求返回的数据，所以即使设为false，也只对HEAD和GET请求有效。
**url**：服务器端网址。这是唯一必需的一个属性，其他属性都可以省略。
**type**：向服务器发送信息所使用的HTTP动词，默认为GET，其他动词有POST、PUT、DELETE。
**dataType**：向服务器请求的数据类型，可以设为text、html、script、json、jsonp和xml。
**data**：向服务器发送的数据，如果使用GET方法，此项将转为查询字符串，附在网址的最后。
**success**：请求成功时的回调函数，函数参数为服务器传回的数据、状态信息、发出请求的原始对象。
**timeout**: 等待的最长毫秒数。如果过了这个时间，请求还没有返回，则自动将请求状态改为失败。
**error**：请求失败时的回调函数，函数参数为发出请求的原始对象以及返回的状态信息。
**complete**：不管请求成功或失败，都会执行的回调函数，函数参数为发出请求的原始对象以及返回的状态信息。
这些参数之中，url可以独立出来，作为ajax方法的第一个参数。也就是说，上面代码还可以写成下面这样。
```javascript
$.ajax('/url/to/json',{
  type: 'GET',
  dataType: 'json',
  success: successCallback,
  error: errorCallback,
  complete: completeCallback
});
function successCallback(json) {
    $('<h1/>').text(json.title).appendTo('body');
},
function errorCallback(xhr, status){
    console.log('出问题了！');
},
function completeCallback(xhr, status){
    console.log('Ajax请求已结束。');
}
```
### Ajax简便写法
ajax方法还有一些简便写法。
**$.get()** : 发出GET请求。
**$.getScript()** : 读取一个JavaScript脚本文件并执行。
**$.getJSON()** : 发出GET请求，读取一个JSON文件。
**$.post()** : 发出POST请求。
**$.fn.load(**) : 读取一个html文件，并将其放入当前元素之中。
一般来说，这些简便方法依次接受三个参数：url、数据、成功时的回调函数。
#### $.get()
对应**HTTP**的**GET**方法。
get方法接受两个参数，分别为服务器端网址和请求成功后的回调函数。
```javascript
$.get('/data/people.html', function(html){
  $('#target').html(html);
});
```
#### $.post()
对应**HTTP**的**POST**方法。
post方法接受三个参数，服务器端网址、发给服务器的数据和请求成功后的回调函数。
```javascript
$.post('/data/save', {name: 'Rebecca'}, function (resp){
  console.log(JSON.parse(resp));
});
```
#### $.getJSON()
ajax方法的另一个简便写法是getJSON方法。当服务器端返回JSON格式的数据，可以用这个方法代替$.ajax方法。
```javascript
$.getJSON('url/to/json', {'a': 1}, function(data){
    console.log(data);
});
```
上面的代码等同于下面的写法。
```javascript
$.ajax({
  dataType: "json",
  url: '/url/to/data',
  data: {'a': 1},
  success: function(data){
    console.log(data);
  }
});
```
#### $.getScript()
$.getScript方法用于从服务器端加载一个脚本文件。
```javascript
$.getScript('/static/js/myScript.js', function() {
    functionFromMyScript();
});
```
上面代码先从服务器加载myScript.js脚本，然后在回调函数中执行该脚本提供的函数。
getScript的回调函数接受三个参数，分别是脚本文件的内容，HTTP响应的状态信息和ajax对象实例。
```javascript
$.getScript( "ajax/test.js", function (data, textStatus, jqxhr){
  console.log( data ); // test.js的内容
  console.log( textStatus ); // Success
  console.log( jqxhr.status ); // 200
});
```
getScript是ajax方法的简便写法，因此返回的是一个deferred对象，可以使用deferred接口。
```javascript
jQuery.getScript("/path/to/myscript.js")
    .done(function() {
        // ...
    })
    .fail(function() {
        // ...
});
```
#### $.fn.load()
$.fn.load不是jQuery的工具方法，而是定义在jQuery对象实例上的方法，用于获取服务器端的HTML文件，将其放入当前元素。由于该方法也属于ajax操作，所以放在这里一起讲。
```javascript
$('#newContent').load('/foo.html');
```
$.fn.load方法还可以指定一个选择器，将远程文件中匹配选择器的部分，放入当前元素，并指定操作完成时的回调函数。
```javascript
$('#newContent').load('/foo.html #myDiv h1:first',
    function(html) {
        console.log('内容更新！');
});
```
上面代码只加载foo.html中匹配“#myDiv h1:first”的部分，加载完成后会运行指定的回调函数。
### Ajax事件
**jQuery**提供以下一些方法，用于指定特定的AJAX事件的回调函数。
**.ajaxComplete()** : ajax请求完成。
**.ajaxError()** : ajax请求出错。
**.ajaxSend()** : ajax请求发出之前。
**.ajaxStart()** : 第一个ajax请求开始发出，即没有还未完成ajax请求。
**.ajaxStop()** : 所有ajax请求完成之后。
**.ajaxSuccess()** : ajax请求成功之后。
下面是示例。
```javascript
$('#loading_indicator')
.ajaxStart(function (){$(this).show();})
.ajaxStop(function (){$(this).hide();});
$('#loading_indicator')
.ajaxStart(function (){$(this).show();})
.ajaxStop(function (){$(this).hide();});
```
### 返回值
ajax方法返回的是一个deferred对象，可以用then方法为该对象指定回调函数。
```javascript
$.ajax({
  url: '/data/people.json',
  dataType: 'json'
}).then(function (resp){
  console.log(resp.people);
});
```
### JSONP
由于浏览器存在“同域限制”，ajax方法只能向当前网页所在的域名发出HTTP请求。但是，通过在当前网页中插入script元素（\<script>），可以向不同的域名发出GET请求，这种变通方法叫做JSONP（JSON with Padding）。
ajax方法可以发出JSONP请求，方法是在对象参数中指定dataType为JSONP。
```javascript
$.ajax({
  url: '/data/search.jsonp',
  data: {q: 'a'},
  dataType: 'jsonp',
  success: function(resp) {
    $('#target').html('Results: ' + resp.results.length);
  }
});
```
JSONP的通常做法是，在所要请求的URL后面加在回调函数的名称。ajax方法规定，如果所请求的网址以类似“callback=?”的形式结尾，则自动采用JSONP形式。所以，上面的代码还可以写成下面这样。
```javascript
$.getJSON('/data/search.jsonp?q=a&callback=?',
  function(resp) {
    $('#target').html('Results: ' + resp.results.length);
  }
);
```