# event

## Dom0 级事件 使用dom.onclick = fun()添加
+ 只在冒泡阶段触发，只能有一个事件，后续添加的事件会覆盖之前的事件,`this指向当前元素`

## Dom2 级事件 addEventListener(type, fn, boolean)
+ 接收三个参数：事件类型（不带“on”）、事件处理函数、一个布尔值（true表示在捕获阶段调用事件处理函数，false表示在冒泡阶段调用事件处理函数；不传第三个参数，默认在冒泡阶段调用事件处理函数。在捕获阶段调用后，不会在冒泡阶段再次调用）。
可以添加多个事件处理函数，按照添加顺序执行。`this指向window`。

# 事件流
+ 在实际中，事件流包括了三个阶段：事件捕获阶段，处于目标阶段，事件冒泡阶段，当点击一个div元素时，以下就是事件流的顺序： 
1. 顶级对象（window）接收到click事件，然后逐级向下捕获 
2. 目标元素（div）接收到到事件 
3. 对事件做出响应，逐级向上冒泡到顶级对象
```javascript
<div class="div1">
      <div class="div2">
        <div class="div3"></div>
      </div>
</div>
<script>
var div1=document.querySelector(".div1")
var div2=document.querySelector(".div2")
var div3=document.querySelector(".div3")
div1.addEventListener('click',function(){ console.log(1) },false)
div2.addEventListener('click',function(){ console.log(2) },true)
div3.addEventListener('click',function(){ console.log(3) },false)
</script>

// 输出结果 2 3 1
```


## 参考链接

- Sebastian Porto, [Asynchronous JS: Callbacks, Listeners, Control Flow Libs and Promises](http://sporto.github.com/blog/2012/12/09/callbacks-listeners-promises/)
- Rhys Brett-Bowen, [Promises/A+ - understanding the spec through implementation](http://modernjavascript.blogspot.com/2013/08/promisesa-understanding-by-doing.html)
- Matt Podwysocki, Amanda Silver, [Asynchronous Programming in JavaScript with “Promises”](http://blogs.msdn.com/b/ie/archive/2011/09/11/asynchronous-programming-in-javascript-with-promises.aspx)
- Marc Harter, [Promise A+ Implementation](https://gist.github.com//wavded/5692344)
- Bryan Klimt, [What’s so great about JavaScript Promises?](http://blog.parse.com/2013/01/29/whats-so-great-about-javascript-promises/)
- Jake Archibald, [JavaScript Promises There and back again](http://www.html5rocks.com/en/tutorials/es6/promises/)
- Mikito Takada, [7. Control flow, Mixu's Node book](http://book.mixu.net/node/ch7.html)
