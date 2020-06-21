## 实现数组的map方法

```javascript
Array.prototype.map = function(callbackFn, initialValue) {
  // 处理数组类型异常
  if (this === null || this === undefined) {
    throw new TypeError("Cannot read property 'map' of null or undefined");
  }
  // 处理回调类型异常
  if (Object.prototype.toString.call(callbackfn) != "[object Function]") {
    throw new TypeError(callbackfn + ' is not a function')
  }
  // 草案中提到要先转换为对象
  let O = Object(this);

  let len = O.length >>> 0;

  let k = 0;
  let accumulator = initiaValue;
  if(initiaValue === undefined){
    for(;k<len;k++){
      if(k in O){
        accumulator = O[k];
        k++;
        break;
      }
    }
    throw new Error("Each element of the array is empty")
  }
  for(;k<len; k++){
      if(k in O){
      accumulator = callbackfn(undefined, accumulator, O[k], O)
      }
  }
  return accumulator;
}

```
