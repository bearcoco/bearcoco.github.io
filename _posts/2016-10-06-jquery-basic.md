---
layout:     post
title:      "jQuery基本知识"
subtitle:   ""
date:       2016-10-06
author:     "zgx"
header-img: "img/post-bg-js-version.jpg"
catalog: true
tags:
    - jQuery
---

## jQuery的入口函数

``` js 
方式一：
$(document).ready(function(){
    // 功能代码
});
方式二：
$(function(){
    // 功能代码
});
```
## jQuery入口函数与js入口函数的区别

js入口函数指的是：window.onload = function() {}; 
区别：
- 1、书写个数不同<br>
Js入口函数只能出现一次，出现多次会存在事件覆盖的问题。<br>
jQuery的入口函数，可以出现任意多次，并不会存在事件覆盖问题。<br>
- 2、执行时机不同<br>
Js入口函数是在所有的文件资源加载完成后，才执行。<br>
这些文件资源包括：页面文档、外部的js文件、外部的css文件、图片等。<br>
jQuery的入口函数，是在文档加载完成后，就执行。文档加载完成指的是：DOM树加载完成后，就可以操作DOM了，
不用等到所有的外部资源都加载完成。
- 文档加载的顺序：从上往下，边解析边执行。

## jQuery的$符号

- jQuery里面的$符号实际上是一个函数
``` js 
// jQuery里面使用$的方式
$(document).ready(function(){ }); // 调用入口函数
$(function(){ });                 // 调用入口函数
$("#btnShow")                     // 获取id属性为btnShow的元素
$("div")                          // 获取所有的div元素
```

jQuery里面的$函数，根据传入参数的不同，进行不同的调用，实现不同的功能。返回的是jQuery对象。<br>
jQuery这个js库，除了$之外，还提供了另外一个函数：jQuery<br>
jQuery函数跟$函数的关系：jQuery === $   => true<br>


## jQuery对象和DOM对象的相互转换
- DOM对象
``` js
var btn = document.getElementById("btnShow"); // btn就是一个DOM对象
```
- jQuery对象
``` js
var $btn = $("#btnShow"); // $btn就是一个jQuery对象
```
- Query对象是包装的DOM对象的集合，即：包装集
- DOM对象转换成jQuery对象：
``` js 
var $btn = $(btn); // 此时就把DOM对象btn转换成了jQuery对象$btn
```
- jQuery对象转换成DOM对象：
``` js 
// 方式一
var btn1 = $btn[0]; // 此时就把jQuery对象$btn转换成了DOM对象btn1 （推荐使用此方式）
// 方式二
var btn2 = $btn.get(0);// 此时就把jQuery对象$btn转换成了DOM对象btn2
```

## jQuery选择器
常用的选择器汇总

``` 
*               $("*")              所有元素
#id             $("#lastname")      id="lastname" 的元素
.class          $(".intro")         所有 class="intro" 的元素
element         $("p")              所有 <p> 元素
.class.class    $(".intro.demo")    所有 class 具有 "intro" 且 "demo" 的元素
s1,s2,s3        $("th,td,.intro")   所有带有匹配选择的元素
:even           $("tr:even")        所有偶数 <tr> 元素
:odd            $("tr:odd")         所有奇数 <tr> 元素
:first          $("p:first")        第一个 <p> 元素
:last           $("p:last")         最后一个 <p> 元素
:eq(index)      $("ul li:eq(3)")    列表中的第四个元素（index 从 0 开始）
:gt(index)      $("ul li:gt(3)")    列出 index 大于 3 的元素 greater than
:lt(index)      $("ul li:lt(3)")    列出 index 小于 3 的元素 less than
:not(selector)  $("input:not(:empty)")  所有不为空的 input 元素

:header         $(":header")        所有标题元素 <h1> - <h6>
:animated       $(":animated")      所有正在执行动画的元素
:contains(text)     $(":contains('W3School')")  包含指定字符串的所有元素
:empty              $(":empty")                 无子（元素）节点的所有元素
:hidden             $("p:hidden")               所有隐藏的 <p> 元素
:visible            $("table:visible")          所有可见的表格
[attribute]         $("[href]")         所有带有 href 属性的元素
[attribute=value]   $("[href='#']")     所有 href 属性的值等于 "#" 的元素
[attribute!=value]  $("[href!='#']")    所有 href 属性的值不等于 "#" 的元素
[attribute$=value]  $("[href$='.jpg']") 所有 href 属性的值包含以 ".jpg" 结尾的元素
:input              $(":input")         所有 <input> 元素
:text               $(":text")          所有 type="text" 的 <input> 元素
:password           $(":password")      所有 type="password" 的 <input> 元素
:radio              $(":radio")         所有 type="radio" 的 <input> 元素
:checkbox           $(":checkbox")      所有 type="checkbox" 的 <input> 元素
:submit             $(":submit")        所有 type="submit" 的 <input> 元素
:reset              $(":reset")         所有 type="reset" 的 <input> 元素
:button             $(":button")        所有 按钮元素（<button></button> 或者 input="button"）
:image              $(":image")         所有 type="image" 的 <input> 元素
:file               $(":file")          所有 type="file" 的 <input> 元素
:enabled            $(":enabled")       所有激活的 input 元素
:disabled           $(":disabled")      所有禁用的 input 元素
:selected           $(":selected")      所有被选取的 input 元素
:checked            $(":checked")       所有被选中的 input 元素
```

## jQuery选择方法
- 获取父级元素
```
$(selector).parent();     //获取直接父级
$(selector).parents('p'); //获取所有父级元素直到html   
```
- 获取子代和后代的元素
```
$(selector).children();   //获取直接子元素
$(selector).find("span"); //获取所有的后代元素  find方法 可能用的多。
```
- 获取同级的元素
```
$(selector).siblings()    //所有的兄弟节点
$(selector).next()        //下一个兄弟节点
$(selector).nextAll()     //后面的所有节点
$(selector).prev()        //前面一个的兄弟节点
$(selector).prevAll()     //前面的所有的兄弟节点
```
- 过滤方法
```
$("p").eq(1);           //取第n个元素
$("div p").last();        //取最后一个元素
$("div p").first();       //取第一个元素
$("p").filter(".intro");  //过滤，选择所有p标签带有 .intro类
$("p").not(".intro");     //去除，跟上面的filetr正好相反
```

## jQuery常用DOM操作

**基本样式属性操作**
- 设置样式属性操作
```
设置单个样式：
// 第一个参数表示：样式属性名称
// 第二个参数表示：样式属性值
$(selector).css("color", "red");
设置多个样式：（也可以设置单个）
// 参数为 {}（对象）
$(selector).css({"color": "red", "font-size": "30px"});
```
- 获取样式属性操作：
```
// 参数表示要获取的 样式属性名称
var fs = $(selector).css("font-size");
```

**类样式操作**

- 添加类样式：
```
作用：为指定元素添加类className
$(selector).addClass("liItem");
```
- 移除类样式：
```
作用：为指定元素移除类 className
$(selector).removeClass("liItem");
$(selector).removeClass(); 不指定参数，表示移除被选中元素的所有类
```
- 判断有没有类样式：
```
作用：判断指定元素是否包含类 className
var hasC = $(selector).hasClass("liItem");
此时，会返回true或false
```
- 切换类样式：
```
作用：为指定元素切换类 className，该元素有类则移除，没有指定类则添加。
$(selector).toggleClass("liItem");
```

**链式编程 和 隐式迭代**
```
$("li").parent("ul").parent("div").siblings("div").children("div").html("内容");
链式编程原理：return this;
通常情况下，只有设置操作才能把链式编程延续下去。因为获取操作的时候，会返回获取到的相应的值，无法返回 this。
end(); // 结束当前链最近的一次过滤操作，并且返回匹配元素之前的一次状态。
隐式迭代
// 设置操作
$("div").css("color", "red");
// 获取操作
$("div").css("color"); // 返回第一个元素的值
隐式迭代的意思是：在方法的内部会为匹配到的所有元素进行循环遍历，执行相应的方法；
而不用我们再进行循环，简化我们的操作，方便我们调用。
````
