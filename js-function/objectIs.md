## 实现Object.is功能
object.is和`===`的区别在于在严格等于的基础上修复了一些特殊情况下的失误，具体来说就是+0和-0，NaN和NaN。
```javascript
function is(x,y){
    if(x===y){
        //运行到1/x === 1/y的时候x和y都为0，但是1/+0 = +Infinity， 1/-0 = -Infinity, 是不一样的
        return x!==0 || y !==0 || 1/x === 1/y
    }
    else{
        return x !==x && y !==y
    }
}

```