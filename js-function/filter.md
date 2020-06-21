## 手写filter方法
```javascript
Array.prototype.filter = function(callbackfn, thisArg ){
    if(!Array.isArray(this || this == null || this== undefined)){
        throw new TypeError("Cannot read property 'filter' of null or undefined")
    }
    if(Object.prototype.toString.call(callbackfn) !== "[object Function]"){
        throw new TypeError(callbackfn + ' is not a function')
    }
    let array = Object(this)
    let len = array.length >>> 0;
    let res = new Array()
    for(let k=0; k< len ; k++){
        if(k in array){
            if(callbackfn.call(thisArg, array[k], k , array))
            res.push(array[k])
        }
    }
    return res;

}


```