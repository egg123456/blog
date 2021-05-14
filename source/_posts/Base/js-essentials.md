---
title: JS - Essentials
date: 2018/5/4
categories:
- base
---
 任何语言的核心都必然会描述这门语言最基本的工作原理。而描述的内容通常是要涉及这门语言的语法、操作符、数据类型，内置更能等用于国建复杂解决方案的基本概念
## theory
+ 是弱类型的语言
+ 所有变量区分大小
    - 字母、下划线、数字、$符号组合的不以数字开头的变量名名称
    - 不能是关键字和保留字
    - 关键字和保留字都是全小写的 eg typeof instanceof
+ Number数据类型使用IEEE754 64位的格式来表示，所以整数和浮点数，浮点数值计算会产生舍入误差问题    eg 0.1+0.2=0.3000000000000004（15个0）

## skill
+ Number 与 String之间的数据装换
    - Number --> String
        - String(num);
        - num.toString();
        - ''+num //加号字符串链接符
    - String --> Number
        - Number(str);  //无进制转换忽略前导0 eg Number('000123') //123S
        - parseInt(str); //忽略前导0，可添加基数进行进制转黄    
            - console.log(parseInt('-12.99px'));//-12
			- console.log(parseInt('px-12.99px'));//nan
			- console.log(parseInt('15e6',10));//e不是数字，取头，十进制15等于15
			- console.log(parseInt('0xf',16));
			- console.log(parseInt('f',16));
			- console.log(parseInt('f',8));//8进制里没有8以上的，所以为nan
        - parseFloat(str)
        - 除加号以外的算术运算符 - * / % 
        - 一元加减操作符   eg +‘12’   -‘12’

+ 类数组--> array
    - Array.prototype.slice.call(arguments)

+ label语句 （定位 跳转）

+ width语句： 将代码的作用域设置到一个特定对象中，他的属性即可做全局变量使用，省略如window.前缀

+ switch case ：case的值可以是常量、变量、表达式，进行的是全等比较

-------
+ data-type
    - typeof 返回基本数据类型、function、object
    - instanceof 返回具体对象，基本类型则返回false
    - Object.prototype.toString.call(data).slice(8,-1); 
    - typeof data检测除null之外的基本数据类型，data instanceof 引用类型 通过原型链搜索是否有，有则返回true
    - data.constructor.name    获得其构造函数的名字

+ Memory
    - 垃圾回收机制： 标记清除/引用清除
    - 管理内存：将无用全局对象（解除引用） person=null；
    - 每个执行环境都有一个预支关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中（在文本浏览器中全局执行环境被认为是window对象

+ 对象的属性访问
    - obj.name
    - obj[name]

+ Array的length属性不是只读的，所以他有修改数组的功能，修改其值数组会自行增加undefined或移除已有值

+ Array迭代方法：arr.every(fn) arr.some(fn) arr.fliter(fn) arr.map(fn) arr.foreach(fn)

+ Array归并方法：arr.reduce(fn) 前两项操作完后的结果在与下一项操作
------
## regexp
+ 实例属性：gim、lastindex、source
+ 实例方法：注意.exec()返回的数组对象
+ 过早函数属性：其属性包含了正则对象使用的具体信息，他们基于所有正则对象所执行的最近一次操作而变化 eg Regexp.input表示最近一次要匹配的字符串
+ 由于gim表全局匹配lastindex属性表示下一次匹配的开始位置--因此引发实例属性不重置问题

## 机制
+ 函数机制
    - this  通常指向调用的对象或执行环境的变量对象
    - arguments 函数的内部属性，包含了传入参数组成类数组对象，通过其完成函数重载
    - arguments.callee 是指向其所在函数的指针，完成函数内部的准确自身调用
    - 记忆自身定义时的环境（闭包）

+ 原型机制
    - 当对象调用函数时，首先会在其自身寻找对应函数，如若没有则通过原型链查找到对应函数
    - 反之，对象通过原型链来进行继承和扩展
    - 注意：父级对象通过对象-属性扩展的属性和方法也是原型内容，且引用类型数据的特征，会使得多个子类共同修改同一个父级值为引用类型的属性---从而推出各模式的继承

+ new机制
    - 当通过new构造函数时，后台会先创建一个空对象，作为要返回的实例对象 - 
    - 将这空对象的原型，指向构造函数的prototype属性
    - 将这个空对象赋值给函数内部的this关键字
    - 开始执行构造函数内部的代码

+ 基本类型使用对象属性、方法机制
    - 每当读取一个基本类型值的时候，后台就会自动创建一个对应的基本包装类型的对象，从而让我们能够调用一些方法来操作这些数据。
    - 在执行完该行之后销毁

```js
    var str = "abc";
    var length = str.length;
    str.color="red";
    console.log(length); //3
    console.log(str.color); //undefined (第三行后台创建的基本数据类型对象及属性，在执行完该行时已被销毁。此处新创建的无赋值)
```


