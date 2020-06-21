## 实现instanceof的功能
instanceof适用于获取对象的类型，typeof 适合于获取基本数据类型
```javascript
function myInstanceOf(left, right){
    if(typeof left !== "object" || left === null) return false;
    let proto = Object.getPrototypeOf(left)
    while(true){
        if(proto==null) return false;
        if(proto == right.prototype) return ture;
        proto = proto.getPrototypeof(proto)

    }
 }

```