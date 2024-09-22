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

### 发布订阅模式
用于事件调度。如 eventEmitter 一样。
```js
// 公众号对象
let eventEmitter = {};

// 缓存列表，存放 event 及 fn
eventEmitter.list = {};

// 订阅
eventEmitter.on = function (event, fn) {
    let _this = this;
    // 如果对象中没有对应的 event 值，也就是说明没有订阅过，就给 event 创建个缓存列表
    // 如有对象中有相应的 event 值，把 fn 添加到对应 event 的缓存列表里
    (_this.list[event] || (_this.list[event] = [])).push(fn);
    return _this;
};

// 发布
eventEmitter.emit = function () {
    let _this = this;
    // 第一个参数是对应的 event 值，直接用数组的 shift 方法取出
    let event = [].shift.call(arguments),
        fns = [..._this.list[event]];
    // 如果缓存列表里没有 fn 就返回 false
    if (!fns || fns.length === 0) {
        return false;
    }
    // 遍历 event 值对应的缓存列表，依次执行 fn
    fns.forEach(fn => {
        fn.apply(_this, arguments);
    });
    return _this;
};

function user1 (content) {
    console.log('用户1订阅了:', content);
};

function user2 (content) {
    console.log('用户2订阅了:', content);
};

// 订阅
eventEmitter.on('article', user1);
eventEmitter.on('article', user2);

// 发布
eventEmitter.emit('article', 'Javascript 发布-订阅模式');

```


### 观察者模式
用于监听特定目标的操作，如 dom 事件监听，中间没有发布订阅模式的调度中心
```js
// 主题
class Subject {
  private state: number = 0;
  private observers: Observer[] = [];

  getState(): number {
    return this.state;
  }

  setState(newState: number) {
    this.state = newState;
    this.notify();
  }

  // 添加观察者
  attach(observer: Observer) {
    this.observers.push(observer);
  }

  // 通知所有观察者
  private notify() {
    for (const observer of this.observers) {
      observer.update(this.state);
    }
  }
}

// 观察者
class Observer {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  update(state: number) {
    console.log(`${this.name} update, state is ${state}`);
  }
}

const sub = new Subject();
const observer1 = new Observer("A");
sub.attach(observer1);
const observer2 = new Observer("B");
sub.attach(observer2);

sub.setState(1); // 更新状态，触发观察者 update
```
