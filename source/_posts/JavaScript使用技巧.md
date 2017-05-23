---
title: JavaScript使用技巧
date: 2017-05-19 15:57:58
categories: js 
tags:
---
# JavaScript使用技巧
原文：[http://www.cnblogs.com/jiuyi/p/4226896.html](http://www.cnblogs.com/jiuyi/p/4226896.html)

1、如果 ajax 返回单一的 json 格式，接收方需要这样再格式化一下赋值：

var str = eval("(" + msg + ")");

开发引用： /// <reference path="http://x.autoimg.cn/as/static/js/jquery-1.7.2.min.js" />

2、如果 ajax 同发出两个以上的请求时，返回的状态会串，不能用异步，用同步可以解决问题；

3、navigator.plugins["Shockwave Flash"] 检查 当前机器 flash 版本

4、删除前后空格 String.prototype.trim = function () { return this.replace(/(^[ |　]*)|([ |　]*$)/g, ""); }

5、IE6 下 JS 在执行一个方法后，当前方法内的代码执行完后，此次的单线程就会停止，当前的方法里还有其它的方法也不会再执行；如果要执行的话，需要加 setTimeout(); 事件再执行；

6、把 document.getElementById(id) 转换成 $("id")
function $(id) { return typeof (id) == 'string' ? document.getElementById(id) : id }

7、图片加载失败，并防止死循环 onerror="this.src=aaa.jpg;this.onerror=null;"

8、document.getElementsByTagName('*').length 查看页面有多少个 Dom 元素；

9、parseInt() 只会返回整数部分；一个完整的parseInt应该是这样的：parseInt(string, radix)，其中radix指定数字的进制（十进制，二进制，十六进制etc.） parseInt("f",16): 15

把加号放在包含合法数字的字符串前面会将字符串转化为数字；

Null 用成数字时会表现为0，做布尔时表现为false.

声明一个变量但没有赋值，此时这个变量的值为undefined. Undefined用作数字时类型表现为NaN, 用作布尔时表现为false.

10、各种正则验证规则 数字验证规则：
>  "^\\d+$"　　//非负整数（正整数 + 0）
"^[0-9]*[1-9][0-9]*$"　　//正整数
"^((-\\d+)|(0+))$"　　//非正整数（负整数 + 0）
"^-[0-9]*[1-9][0-9]*$"　　//负整数
"^-?\\d+$"　　　　//整数
"^\\d+("　　//非负浮点数（正浮点数 + 0）
"^(([0-9]+\\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\\.[0-9]+)|([0-9]*[1-9][0-9]*))$"　　//正浮点数
"^((-\\d+("　　//非正浮点数（负浮点数 + 0）
"^(-(([0-9]+\\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\\.[0-9]+)|([0-9]*[1-9][0-9]*)))$"　　//负浮点数
"^(-?\\d+)("　　//浮点数
var r = /^\+?[1-9][0-9]*$/;　　//正整数
r.test(str); 

11、按照 json 的属性值排序
> var cc=[
{ name: "a", age: 30},
{ name: "c", age: 24},
{ name: "b", age: 28},
{ name: "e", age: 18},
{ name: "d", age: 38}
].sort(function(obj1, obj2) {
return obj1.age - obj2.age;
});
for(var i=0;i<cc.length;i++){
alert(cc[i]['age']); //依次显示 18,24,28,30,38
}

13、多点击事件获取点击的是哪个
> $('#IndexLink,#IndexLink1').on('click', function (e) {
var id=e.target.id;
//id 取到的就是被点击的ID值
}


17、window.history.forward(1); 阻止页面后退；

18、 JS call 与aplly 用法
> function Person(name, age) {
this.name = name;
this.age = age;
};

function Student(name, age, grade) {
Person.apply(this, arguments);
this.grade = grade;
};
var student = new Student('qian', 21, '一年级');
alert('name:' + student.name + '\n' + 'age:' + student.age + '\n' + 'grade:' + student.grade);

//也就是通俗一点讲就是:用student去执行Person这个类里面的内容,在Person这个类里面存在this.name等之类的语句,
//这样就将属性创建到了student对象里面

页面到底部自动加载内容：
> var divH = document.body.scrollHeight,top = document.body.scrollTop,windowH = window.screen.availHeight;
if ((top + windowH) >divH) {
console.log('该他妈的加载内容了。');
}
console.log('网页正文全文高：' + document.body.scrollHeight + ' 网页被卷去的高： ' + document.body.scrollTop + ' 屏幕可用工作区高度:' + window.screen.availHeight);

