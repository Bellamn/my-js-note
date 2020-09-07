## 柯里化
+ 创建简短的“偏应用函数（partially applied function）”或“偏函数（partial）”。
```javascript
function curry(func){
    return function curried(...args) {
    if (args.length >= func.length) {
      return func.apply(this, args);
    } else {
      return function(...args2) {
        return curried.apply(this, args.concat(args2));
      }
    }
  };
}
```