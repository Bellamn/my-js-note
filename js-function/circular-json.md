## 用于处理循环引用的对象序列化函数
```javascript
censor(censor) {
    var i = 0;
    return function(key, value) {
        if(i !== 0 && typeof(censor) === 'object' && typeof(value) == 'object' && censor == value) 
        return '[Circular]'; 

        if(i >= 29) // seems to be a harded maximum of 30 serialized objects?
        return '[Unknown]';

        ++i; // so we know we aren't using the original object anymore

        return value;  
    }
}

var b = {foo: {bar: null}};

b.foo.bar = b;

console.log("Censoring: ", b);

console.log("Result: ", JSON.stringify(b, censor(b)));

```