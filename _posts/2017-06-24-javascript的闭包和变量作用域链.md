---
layout: post
title: javascript的闭包和变量作用链域
date: 2017-06-24
categories: javascript
tags: [jQuery]
---

用了很久的js但一直没真正理解js的闭包，今天好好查了书籍和资料终于豁然开朗，总结一下。
### 什么是闭包？
以前一直蠢蠢地认为闭包是js里面的一种函数类型，不知道有多少朋友会和我一样chun<img src="http://img.baidu.com/hi/face/i_f18.gif"/>。言归正传，闭包其实是指一种特性——“函数可以通过作用链域关联起来，函数内部的变量都保存在函数的作用域内。也就是说函数变量可以隐藏于函数作用链域之内，看起来就像是函数将变量包了起来。”

下面的例子可以感受一下这个特性：
```
function getGirl(){
    var girl = 'Lily';
    function f(){
        return girl;
    }

    return f();
}

getGirl();  //return Lily
```

上面的函数我们很好理解，getGirl()返回的是f()的执行结果，所以返回的是getGirl()的局部变量Lily。我们再看看下一个：
```
function getGirl(){
    var girl = 'Lily';
    function f(){
        return girl;
    }

    return f;
}

getGirl()();  //返回值是什么？
```
这个例子我们把一对圆括号移到了getGirl()之后，getGirl()只返回一个函数对象，而不是直接返回结果。在定义函数getGirl()的作用域外面调用，会发生什么？

想法1:既然是在getGirl()的函数作用域之外调用，那么此时调用的girl应该不再是局部变量而是全局变量，所以此时返回的是&#39;Summer&#39;。听起来很对的样子，但真的去运行一下就啪啪打脸了（结果见下图），如果读者也是和想法1一样的思路那么也就是和我之前一样并没有完整理解闭包这个特性，也就有继续看下去的必要了。

<img src="http://blog.luojia.ren/upload/1491492778746.jpeg" title="WechatIMG2.jpeg"/>

要想通这个问题我们必须要理解函数的作用域链，了解这个问题之前，我们先了解一下js的全局变量和局部变量。我们知道在js中变量分为全局变量和局部变量，全局变量可以看成是全局对象的一个属性。
```
var master = 'Summer';
console.log(this.master);   //Summer
```
全局变量是全局对象的属性，这是在ECMAScript规范中强制规定的。对于局部变量，虽然没有类似的强制规定，但我们可以想象，局部变量可以当作是一个和函数调用相关的对象的属性，也就是还是某个对象的属性，ECMAScript3规范中称该对象为“调用对象”，ECMAScript5规范称为“声明上下文对象”，但本质还是个对象。

如果把局部变量看成是一个自定义实现的对象的属性的话，那么可以换个角度来看变量作用域。每一段全局代码或者函数都有一个与之相关联的作用域链，这个作用链域是一个对象列表或者链表，每次调用javascript函数的时候，都会为之创建一个新的对象来保存局部变量并把这个对象添加到作用链域中。当javascript需要查找变量x的时候，它会从链表的第一个对象开始查找，如果这个对象中有x属性则返回，反之则继续查找下一个对象，依次类推，如果作用链域没有一个对象含有属性x的话，就认为这段代码的作用链域上不存在x，抛出引用错误。对于上一个例子，在作用链域上f()调用对象是第一个对象，getGirl()对象是第二个对象，全局对象是第三个对象，作用链域在函数定义的时候就已经决定，所以当用户在函数作用域之外调用嵌套函数f()的时候，js的变量解析依旧和在getGril()内直接调用f()时的解析顺序是一致的。
现在再回想一下闭包特性的定义——“函数可以通过作用链域关联起来，函数内部的变量都保存在函数的作用域内。也就是说函数变量可以隐藏于函数作用链域之内，看起来就像是函数将变量包了起来”。现在再看这句话是否已经能够更深地理解了？简而言之，闭包的这个特性可以捕捉到局部变量和参数，并一直保留下来。

可以再看一个计数器的例子：
```
function counter(){
    var n = 0;
    return {
        count: function(){return n++;},
        reset: function(){n = 0;}
    };
}

var a = counter(), b = counter();
a.count();   //1
b.count();   //1
a.reset();   //0,reset()和count()共享状态
a.count();    //1
b.count();    //2 ;a,b互不干扰，a的重置不影响b
```
如上代码所示，counter()函数返回一个计数器对象，理解如下点：

1.这个对象包含两个方法，两个方法都可以访问私有变量
2.每次调用count()都会创建一个新的作用链域和一个新的私有变量
3.调用多个count()会得到多个计数器对象，彼此包含不同的私有变量，对象之前不会相互影响
	
> {{ page.date | date_to_string }}，原创文章，转载请注明出处