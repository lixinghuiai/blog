---
title: JavaScript 格式化数字、金额、千分位、保留几位小数、舍入舍去…
date: 2017-05-20 14:51:54
categories: "js" 
tags:
---
# JavaScript 格式化数字、金额、千分位、保留几位小数、舍入舍去…
 #### 将数值四舍五入(保留2位小数)后格式化成金额形式
 
``` 
function formatCurrency(num) {
    num = num.toString().replace(/\$|\,/g,'');
    if(isNaN(num))
        num = "0";
    sign = (num == (num = Math.abs(num)));
    num = Math.floor(num*100+0.50000000001);
    cents = num%100;
    num = Math.floor(num/100).toString();
    if(cents<10)
    cents = "0" + cents;
    for (var i = 0; i < Math.floor((num.length-(1+i))/3); i++)
    num = num.substring(0,num.length-(4*i+3))+','+
    num.substring(num.length-(4*i+3));
    return (((sign)?'':'-') + num + '.' + cents);
}
```
或者
``` 
function fmoney(s, n) {
    /*
     * 参数说明：
     * s：要格式化的数字
     * n：保留几位小数
     * */
    n = n > 0 && n <= 20 ? n : 2;
    s = parseFloat((s + "").replace(/[^\d\.-]/g, "")).toFixed(n) + "";
    var l = s.split(".")[0].split("").reverse(),
        r = s.split(".")[1];
    t = "";
    for (i = 0; i < l.length; i++) {
        t += l[i] + ((i + 1) % 3 == 0 && (i + 1) != l.length ? "," : "");
    }
    return t.split("").reverse().join("") + "." + r;
}
```
//调用
fmoney(9.7,2);//9.70
fmoney('12345.675910', 3);//12,345.676


#### 更加完善的功能函数

``` function number_format(number, decimals, dec_point, thousands_sep, roundtag) {
    /*
     * 参数说明：
     * number：要格式化的数字
     * decimals：保留几位小数
     * dec_point：小数点符号
     * thousands_sep：千分位符号
     * roundtag:舍入参数，默认 "ceil" 向上取,"floor"向下取,"round" 四舍五入
     * */
    number = (number + '').replace(/[^0-9+-Ee.]/g, '');
    roundtag = roundtag || "ceil"; //"ceil","floor","round"
    var n = !isFinite(+number) ? 0 : +number,
        prec = !isFinite(+decimals) ? 0 : Math.abs(decimals),
        sep = (typeof thousands_sep === 'undefined') ? ',' : thousands_sep,
        dec = (typeof dec_point === 'undefined') ? '.' : dec_point,
        s = '',
        toFixedFix = function (n, prec) {
            var s = n.toString();
            var sArr = s.split(".");
            var m = 0;
            try {
                m += sArr[1].length;
            }
            catch (e) {
            }
 
            if (prec > m) {
                return s;
                /*'' + Number(s.replace(".", "")) / Math.pow(10, m);*/
            } else {
                sArr[1] = Math[roundtag](Number(sArr[1]) / Math.pow(10, m - prec));
                return sArr.join('.');
            }
        };
 
    s = (prec ? toFixedFix(n, prec) : '' + Math.floor(n)).split('.');
    var re = /(-?\d+)(\d{3})/;
    while (re.test(s[0])) {
        s[0] = s[0].replace(re, "$1" + sep + "$2");
    }
 
    if ((s[1] || '').length < prec) {
        s[1] = s[1] || '';
        s[1] += new Array(prec - s[1].length + 1).join('0');
    }
    return s.join(dec);
};
//调用
console.log(number_format(3.7, 2, ".", ","))//"3.70"
console.log(number_format(3, 0, ".", ",")) //"3"
console.log(number_format(9.00, 2, ".", ","))//"9.00"
console.log(number_format(39.715001, 2, ".", ",", "floor")) //"39.71"
console.log(number_format(9.7, 2, ".", ","))//"9.70"
console.log(number_format(39.7, 2, ".", ","))//"39.70"
console.log(number_format(9.70001, 2, ".", ","))//"9.71"
console.log(number_format(39.70001, 2, ".", ","))//"39.71"
```

推荐的类库 [Numeral.js](http://numeraljs.com/) 和 [accounting.js](http://openexchangerates.github.io/accounting.js/)