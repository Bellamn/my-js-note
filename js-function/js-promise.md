## 实现简易的promise
+ resolve 调用将返回值作为参数，调用then传入的回调函数
+ 传入处理结果的回调函数，返回promise对象，
```javascript
function Promise(excutor) {
  this.callbacks = [];

  function resolve(value) {
    setTimeout(() => {
      this.data = value;
      this.callbacks.forEach((callback) => callback(value));
    });
  }

  excutor(resolve.bind(this));
}

Promise.prototype.then = function (onResolved) {
  return new Promise((resolve) => {
    this.callbacks.push(() => {
      const result = onResolved(this.data);
      if (result instanceof Promise) {
        result.then(resolve);
      } else {
        resolve(result);
      }
    });
  });
};
```