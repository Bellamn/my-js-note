## 手写js bind 方法
*** 
1. this绑定
2. 支持柯里化
3. 不丢失原型链

```javascript
Funtion.prototype.bind = functino(context, ...args){
       if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var self = this;

    var fbound = function () {
        self.apply(context, args.concat(Array.prototype.slice.call(arguments)));
    }

    fbound.prototype = Object.create(this.prototype);

    return fbound; 
}
```