---
title: CSS3 transform对普通元素的N多渲染影响
date: 2017-05-19 09:42:03
categories: "css" 
tags: 
    
---
# CSS3 transform对普通元素的N多渲染影响
> 本文地址：[http://www.zhangxinxu.com/wordpress/?p=4799](http://www.zhangxinxu.com/wordpress/?p=4799)
#### transform提升元素的垂直地位
我们可能都知道这样一个规则，当遭遇元素margin负值重叠的时候，如果没有static以外的position属性值的话，后面的元素是会覆盖前面的元素的。例如下面，后面的妹子覆盖了前面的妹子：

``` <img src="mm1"><img src="mm2" style="margin-left:-60px;"> ```

在transform出现之前，这个规则一直很稳健；但是，自从transform降临，这个规则就变了。元素应用了transform属性之后，就会变得应用了position:relative一个尿性，原本应该被覆盖的元素会雄起，变成覆盖其他元素，修改为如下代码：

``` <img src="mm1" style="-ms-transform:scale(1);transform:scale(1);"><img src="mm2" style="margin-left:-60px;"> ```

[CSS3 transform覆盖后面的重叠元素Demo](http://www.zhangxinxu.com/study/201505/css3-transform-cover.html)

#### transform限制position:fixed的跟随效果

我们应该都知道，position:fixed可以让元素不跟随浏览器的滚动条滚动，而且这种跟随效果连它的兄弟们position:relative/absolute都限制不了。但是，真是一物降一物，position:fixed固定效果却被小小的transform给干掉了，直接降级变成position:absolute的蛋疼表现。

``` <p style="transform:scale(1);"><img src="mm1.jpg"style="position:fixed;" /></p> ```

<font color="red"> 注意，这个特性表现，目前只在Chrome浏览器/FireFox浏览器下有，IE浏览器，包括IE11, fixed还是fixed的表现。</font>

#### transform改变overflow对absolute元素的限制
在以前，overflow与absolute之间的限制规范内容大致是这样的：
> absolute绝对定位元素，如果含有overflow不为visible的父级元素，同时，该父级元素以及到该绝对定位元素之间任何嵌套元素都没有position为非static属性的声明，则overflow对该absolute元素不起作用。

 <p style="width:96px; height:96px; border:2px solid #beceeb; overflow:hidden;">
    <img src="mm1.jpg"style="position:absolute;" /></p> 

结果是这样子，图片溢出的右侧还是可见的。

 ![](http://image.zhangxinxu.com/image/study/s/s128/mm1.jpg)
 
但是，一旦我们给overflow容器或者与图片有嵌套关系的子元素使用transform声明，呵呵呵，估计absolute元素就要去领便当了！

比方说，下面这个嵌套一层block水平标签应用transform属性后的效果：
![](http://image.zhangxinxu.com/image/study/s/s128/mm1.jpg)

这里地方小，借一步说话，您可以狠狠地点击这里[transform对overflow absolute元素限制Demo](http://www.zhangxinxu.com/study/201505/css3-transform-overflow.html)

结果出现了有意思的浏览器兼容性差异：Chrome/Opera浏览器下，只有嵌套元素含有transform属性的时候，absolute元素才会被overflow隐藏；但是在IE9+/FireFox浏览器下，无论是overflow容器还是嵌套子元素，只要有transform属性，就会hidden溢出的absolute元素。

截图如下：
 [](http://image.zhangxinxu.com/image/blog/201505/2015-05-21_010034.png)


