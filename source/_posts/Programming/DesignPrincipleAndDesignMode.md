---
title: Design principle and design mode
date: 2018/5/5
categories:
- programming
---

# design principle
设计原则存在根本原因是为了代码复用，增加可维护性。有如下原则：
1. 【开闭原则】对扩展开放，对修改关闭。
2. 【里氏转换原则】子类继承父类，单独调完全可以运行
3. 【依赖倒转原则】引用一个对象，如果这个对象有底层类型，直接引用底层
4. 【接口隔离原则】每一个借口应该是一种角色。
5. 【合成/聚合服用原则】新的对象应使用一些已有的对象，使之成为新对象的一部分。

# design mode
设计模式是一套被反复使用、思想成熟、经过分类和无数实战设计经验的总结。使用设计模式是为了让系统代码可服用、可扩展、可解藕、更容易被人理解且能保证代码可靠性。设计模式使代码开发真正工程化；设计模式是软件工程的基石脉络，如同大厦的结果一样。

### 单例模式
定义：一个类只有一个实例，即使多次实例化该类，也只会返回第一次实例化后的对象。
```js
    const SingleTon = function(name){
        this.name = name;
    }

    SingleTon.prototype.getName = function() {
        console.log(this.name)
    }

    SingleTon.getInstance = function(name){
        if(!this.instance){
            this.instance = new SingleTon(name);
        }
        return this.instance;
    }


    let s1 = SingleTon.getInstance('s1');
    let s2 = SingleTon.getInstance('s2');
    console.log(s1 === s2); //true
```

### 构造函数模式
用于创建特定类型的对象，并能给对象赋值
```js
    function CreateDoor(material = '木', color = '红色') {
        if (!(this instanceof CreateDoor)) {
            return new CreateDoor;
        }
        this.material = material;
        this.color = color;
        this.descript = function() {
            console.log(`我是一扇${color}的${material}门`)
        }
    }
    CreateDoor().descript();
```

