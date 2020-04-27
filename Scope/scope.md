# Scope

## ES6 new feature let
+ 和传统的var声明变量不同，不管出现在什么位置，var都是归属于包含它的`整个函数作用域`。let声明归属于块作用域，但是直到在块中出现才会被初始化。在let声明/初始化之前访问let声明的变量会导致错误，而使用var的话这个顺序是无关紧要的.
+ 过早访问let声明的引用导致的这个ReferenceError严格说叫作临时死亡区（Temporal Dead Zone, TDZ）错误
```javascript
{
//a为用let声明，可以正常运行
if (typeof a==="undefine d"){
    console.log（"cool")；
}
//b声明了，但还处于TDZ
if (typeof b==="undefine d"){
    ////////ReferenceError!  
}
//.
let b；
}
```

### let和for循环
+ for循环头部的let i不只为for循环本身声明了一个i，而是为循环的每一次迭代都重新声明了一个新的i。if语句包含了块作用域变量b和c，块作用域变量i和j存在于for循环之中。 `i并不在包含它的if语句作用域中`
 ``` javascript
let a = 2;
if(a>1){
    let b = a * 3;
    console.log(b); //6
    for(let i=a; i<=b; i++){
        let j=i+10;
        console.log(j) // 12 13 14 15 16
    }
    let c = a + b;
    console.log(c); //8 
}
```
## 块作用域函数
+ foo()函数声明在{ .. }块内部，ES6支持块作用域。所以在块外不可用。但是还要注意到它是在块内“提升”了，与let声明相反，后者会遇到前面介绍的TDZ错误陷阱。

```javascript
{
    foo();
    function foo(){
        // ...
    }
}
foo();
// ReferenceErrorError
```

+ 在前ES5环境中，不管something的值是什么，foo()都会打印出"2"，因为两个函数声明都被提升到了块外，第二个总是会胜出。但在ES6环境中则会报，ReferenceError

```javascript
if(something){
    function foo(){
            console.log("1");
    }
else{
    function foo(){
            console.log("2")；
    }}
foo();//??
```




## 参考链接

- Sebastian Porto, [Asynchronous JS: Callbacks, Listeners, Control Flow Libs and Promises](http://sporto.github.com/blog/2012/12/09/callbacks-listeners-promises/)
- Rhys Brett-Bowen, [Promises/A+ - understanding the spec through implementation](http://modernjavascript.blogspot.com/2013/08/promisesa-understanding-by-doing.html)
- Matt Podwysocki, Amanda Silver, [Asynchronous Programming in JavaScript with “Promises”](http://blogs.msdn.com/b/ie/archive/2011/09/11/asynchronous-programming-in-javascript-with-promises.aspx)
- Marc Harter, [Promise A+ Implementation](https://gist.github.com//wavded/5692344)
- Bryan Klimt, [What’s so great about JavaScript Promises?](http://blog.parse.com/2013/01/29/whats-so-great-about-javascript-promises/)
- Jake Archibald, [JavaScript Promises There and back again](http://www.html5rocks.com/en/tutorials/es6/promises/)
- Mikito Takada, [7. Control flow, Mixu's Node book](http://book.mixu.net/node/ch7.html)
