# hex和rgb颜色转换
## RGB颜色转换为16进制
```javascript
String.prototype.colorHex = function(){
 var that = this;
//十六进制颜色值的正则表达式
var reg = /^#([0-9a-fA-f]{3}|[0-9a-fA-f]{6})$/;
// 如果是rgb颜色表示
if (/^(rgb|RGB)/.test(that)) {
    var aColor = that.replace(/(?:\(|\)|rgb|RGB)*/g, "").split(",");
    var strHex = "#";
    for (var i=0; i<aColor.length; i++) {
        var hex = Number(aColor[i]).toString(16);
        if (hex === "0") {
            hex += hex;	
        }
        strHex += hex;
    }
    if (strHex.length !== 7) {
        strHex = that;	
    }
    return strHex;
} else if (reg.test(that)) {
    var aNum = that.replace(/#/,"").split("");
    if (aNum.length === 6) {
        return that;	
    } else if(aNum.length === 3) {
        var numHex = "#";
        for (var i=0; i<aNum.length; i+=1) {
            numHex += (aNum[i] + aNum[i]);
        }
        return numHex;
    }
}
return that;
};

```
## 16进制转RGB
```javascript
String.prototype.colorRgb = function(){
var sColor = this.toLowerCase();
//十六进制颜色值的正则表达式
var reg = /^#([0-9a-fA-f]{3}|[0-9a-fA-f]{6})$/;
// 如果是16进制颜色
if (sColor && reg.test(sColor)) {
    if (sColor.length === 4) {
        var sColorNew = "#";
        for (var i=1; i<4; i+=1) {
            sColorNew += sColor.slice(i, i+1).concat(sColor.slice(i, i+1));	
        }
        sColor = sColorNew;
    }
    //处理六位的颜色值
    var sColorChange = [];
    for (var i=1; i<7; i+=2) {
        sColorChange.push(parseInt("0x"+sColor.slice(i, i+2)));	
    }
    return "RGB(" + sColorChange.join(",") + ")";
}
return sColor;
};

```

## 方法二  
```javascript
// Check Functions
function checkHex(hex) {
  const hexRegex = /^[#]*([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$/i
  if (hexRegex.test(hex)) {
    return true;
  }
}
 
function checkRgb(rgb) {
  const rgbRegex = /([R][G][B][A]?[(]\s*([01]?[0-9]?[0-9]|2[0-4][0-9]|25[0-5])\s*,\s*([01]?[0-9]?[0-9]|2[0-4][0-9]|25[0-5])\s*,\s*([01]?[0-9]?[0-9]|2[0-4][0-9]|25[0-5])(\s*,\s*((0\.[0-9]{1})|(1\.0)|(1)))?[)])/i
  if (rgbRegex.test(rgb)) {
    return true
  }
}
// Parse Function
function modifyHex(hex) {
  if (hex.length == 4) {
    hex = hex.replace('#', '');
  }
  if (hex.length == 3) {
    hex = hex[0] + hex[0] + hex[1] + hex[1] + hex[2] + hex[2];
  }
  return hex;
}
 
// Converting Functions
function hexToRgb(hex) {
  let x = [];
  hex = hex.replace('#', '')
  if (hex.length != 6) {
    hex = modifyHex(hex)
  }
  x.push(parseInt(hex.slice(0, 2), 16))
  x.push(parseInt(hex.slice(2, 4), 16))
  x.push(parseInt(hex.slice(4, 6), 16))
  return "rgb(" + x.toString() + ")"
}
 
function rgbToHex(rgb) {
  let y = rgb.match(/\d+/g).map(function(x) {
    return parseInt(x).toString(16).padStart(2, '0')
  });
  return "#"+y.join('').toUpperCase()
}
```