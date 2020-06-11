## 用于将查询字符串压缩
+ 利用了replace函数
+ 以及正则表达式，全局匹配和捕获
```javascript
function compress(source){
    const keys = {}
    source.replace(
        /([^=&]+)=([^&]*)/g,
        function(full, key, value){
            console.log(full,key, value)
            keys[key] = (keys[key] ? keys[key] + ',' : "") + value;
            return '';
        }
    )
    const result = {};
    for(let key in keys){
        result.push(key + "=" + keys[key]);
    }
    return result.join("&")
}

conpress("foo=1&foo=2&blah=a&blah=b&foo=3")  // "foo=1,2,3&blah=a,b"

```