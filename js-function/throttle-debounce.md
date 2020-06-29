## 防抖函数
 反复点击按钮只有最后一次生效（从点击到执行中间有时间间隔）
+ 使用settimeout实现, 判断一定时间内如果timer不是null则清除
+ 使用闭包存储timer，并返回函数, 本质是用（闭包和时间来进行状态转移，闭包用来记住状态，时间用来判断转移）
```javasscript
function debounce(fn, delay){
    let timer = null;
    return function(...arg){
        let context = this;
        if(timer !== null) clearTimeout(timer)
        timer = setTimeout(function(){
            fn.apply(context, args);
        }, delay)
    }
}
```
## 节流函数
 + （ 一定时间内只能触发一次）如果在定时器的时间范围内再次触发，则不予理睬，等当前定时器完成，才能启动下一个定时器任务。
```javasscript
function throttle(fn, delay){
    let flag=true;
    return function(...arg){
        let context = this;
        if(!false) return;
        let flag = false
        if(flag) {        
            timer = setTimeout(function(){
            fn.apply(context, args);
            flag=true}
            , delay)}
    }
}
```
+更好的实现方式, 第一次点击立马执行
```javasscript
function throttle(fn, delay){
    let timer;
    return funtion(...args){
        let now = new Date()
        let last = timer;
        if(!last){
            timer = now;
            fn.apply(this, args)
        }
        if(last + delay < now) return;
        timer = now;
        fn.apply(this, args)
    }

```

## 防抖和节流结合
+ 防抖会导致，如果用户一直频繁点击，会一直得不到响应；加强版使得其可以在一定时间内响应一次。

```javasscript
function debouncePlus(fn, delay){
    let timer = null， last = 0;
    return function(...args){
        let cotext=this;
        let now = new Date();
        if(now - last < delay){
            if(timer !== null) clearTimeout(timer);
            setTimeout(function(){
                last = new Date()
                fn.apply(context, args)
            }, delay)
        }
        else{
            last = new Date()
            fn.apply(context, args)
        }
    }

}
```
  