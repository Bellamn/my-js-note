# 实现js call，apply方法
## 此方法不能反应底层原理，且该方法实现中call和apply 一样
```javascript
Function.prototype.call = function(context, ...args) {
  var context = context || window;
  context.fn = this;

  var result = context.fn(...args);

  delete context.fn
  return result;
}
``` 