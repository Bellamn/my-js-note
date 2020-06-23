## 手写js new 方法
*** 
1. 创建一个新对象，
2. 将实例对象的原型指向构造函数原型（引用关系）
3. 将新对象作为上下文，调用构造函数
4. 如果函数没有返回其他对象，那么new表达式中的函数调用会自动返回这个新对象。
```javascript
function newFactory(ctor, ...args){
    if(type ctor !== "function"){
        throw new Error("the first param must be a function")
    }
    let obj = Object.create(ctor.prototype);
    let result = ctor.apply(obj, args)
    return result instanceof Object ? result : obj
}

}
```