---
title: laya
date: 2018/5/2
categories:
- jsLibrary
---

## 结构
+ stage
+ sprite
+ scene
+ node


## 节点添加 实例（script）
```js
// add component instance
this.owner.addComponent(instance);

// get component instance
this.owner.getComponent(instance);
```


## owner properties
```js
this.owner.name
this.owner.width
this.owner.height
```

## component properties (编辑器的绑定)
```js
/** @prop{name: speed,tips:"速度",type:"类型Int、Number、String、Bool、、、, default:"默认值"} */

this.speed
```

## 节点操作
```js
// instance node
this.owner

// get parent node 
this.owner.parent

// get child by name or index
this.owner.getChildByName();
this.owner.getChildAt();

// child index of parent
this.owner.getChildIndex();

// child array
this.owner._children
// child array length 
this.owner.numChildren

// get current node's scene
this.owner.scene

// add child node 
this.owner.addChild(node);
this.owner.addChildren([node]);
```

## image 组件 九宫格（区域放大问题）
> 图片默认 为image类型 拥有sizeGrid属性

## handle
```js
const h = handle.create('hello world !', function(name, age) {
    console.log(this); // hello world !
    console.log(name, age); // egg 24
})
h.runWith(egg, 24)
```

## laya 事件
> laya 事件和html 事件相似，有冒泡和stopPropogation，事件绑定可通过脚本里的onxxx绑定，也可node.onxxx绑定，效果一样


## fontclip 组件 等宽位图切割


## 定位（坐标空间）
> 节点坐标系： 位置都是相对于父节点的左上角
```js
ver p = new Laya.ponit.create();
p.x = 100;
p.y = 200;
// 获得img xy 位置 在text上的位置
this.img.localToGlobal(p, false, this.text)
// 获得text xy 位置 在img上的位置
this.img.globalToLocal(p, false, this.text)
// tips: this.text 不传默认舞台
```

## 定时器-Laya.time
> laya 有两种类型的定时器，基于帧数的计时器，基于时间的计时器

```js
const func = function (a, b, c) {
    console.log(a, b, c)
}
const func1 = function () {
    console.log(345)
}
// 60帧后触发func
Laya.timer.frameOnce(60, this, func, [1, 2, 3]);
// 每60帧后触发func
Laya.timer.frameLoop(60, this, func);

// 1000毫秒后触发func
Laya.timer.once(1000, this, func1);
// 每1000毫秒帧后触发func
Laya.timer.Loop(1000, this, func1);

// 清理timer func
Laya.timer.clear(this, func);
// 清理所有timer 
Laya.timer.clearAll(this);

// 下一帧执行 func
Laya.timer.callLater(this, func);
// 立即执行func 并删除绑定func 的timer
Laya.timer.runTimer(this, func);

// 时间缩放 Laya.timer.scale
// 因scale = 0.5 所以4000/0.5 = 8000毫秒后执行func
Laya.timer.scale = 0.5;
Laya.timer.once(4000, this. func);
// 因scale = 2 所以4000/2 = 2000毫秒后执行func
Laya.timer.scale = 2;
Laya.timer.once(4000, this. func);

// 当前已过的游戏帧数
Laya.timer.currFrame
// 时间戳
Laya.timer.currTime
// 距离上次update的时间
Laya.timer.delta

```

## 缓动对象
```js
// 从x： 300 处 经过三秒到当前位置
Laya.Tween.from(node, { x: 300 }, 3000)；
// 当前位置 经过三秒到 到x： 300 处 
const t = Laya.Tween.to(node, { x: 300 }, 3000)；
t.progress = 0.5 // 设置动画开始比例
t.repeat = 3 // 重复3次 0为重复无限次

// 清除缓动
t.clear()
Laya.Tween.clear(t);
Laya.Tween.clearAll(node)   // 清除node上的所有缓动
t.complete() // 直接到目标转台

// tips: Laya.Ease.xxx 缓动类型
```

## 自定义事件
```js
// 触发玩家 1000金币的 man_rect 接收事件
this.owner.event("man_recv", [1000, 'coin'])

const func = function(a, b) {
    console.log(a, b, 'man_recv');
}
// 玩家监听 接收事件
this.man.on("man_recv", this, func)

this.man.once("man_recv", this, function(a, b) { //只监听一次
    console.log(a, b, 'man_recv');
})

this.man.off('man_recv', this, func) // 取消监听器func
this.man.offAll('man_recv') // 取消所有监听器
this.man.offCaller(this) // 取消target 为this的所有事件监听
```

### timelien
```js
// 一秒 缩小 延迟2s后 3s 放大
const timeline = Laya.TimeLine.to(this.man, {scaleX: 0, scaleY: 0}, 1000, nul, 2000);
tiemline.to(this.man, {scaleX: 1, scaleY: 1}, 3000)
tiemline.play(0) // 播放一次
tiemline.play(0, true) // 无限次
timeline.destroy() // 取消timeline动画

// timeline 播放完后会触发 complete 事件
timeline.on(Laya.Event.COMPLETE, this, function() {
    console.log('timeline complete')
})

```

### 滤镜
> laya 中有 颜色滤镜、模糊滤镜、发光滤镜
```js
const filter = new Laya.colorFIlter();
filter.serColor('#ff000');
this.man.filter = [f]
```


### soundmanager
```js
// 默认讯黄播放
const sm = Laya.SoundManager.playMusic('sounds/bg.mp3', 1, completeCallback);
Laya.SoundManager.setMusicVolume(0.5);

Laya.SoundManager.playSound('sounds/click.wav');
Laya.SoundManager.serSoundVolume(0.5)

```

### 资源加载
> 游戏资源加载后，使用更快，所以一般的游戏开始前都预加载资源，laya也是可以加载资源，并且可对资源分组管理
```js
// load resource
Laya.loader.load(["res/bg.img","res/bg.mp3"]);
// divide into groups
Laya.loader.setGroup("res/bg.img", 'bg')
Laya.loader.setGroup("res/bg.mp3", 'bg')
// get resouce
Laya.loader.getRes('res/bg.img')
// clear resource
Laya.loader.clearRes('res/bg.img')
// 清理分组中的资源
Laya.loader.clearResBayGroup('bg')
// error handle
Laya.loader.on(Laya.Event.ERROR, this, function(err_url) {
    console.log(err_url)
})

```

### 预制体、图集、帧动画
> 节点与其子节点可生产预制（节点组装）；laya编译后会将散图打包成图集（精灵图）；laya动画加载图集，然后在一张的播放，形成帧动画
```js
// create prefab
const node = this.pre_fab.create();
this.owner.addChild(node);
node.x = 100;
node.y = 100; 

Laya.loader.load('res/atlas/cow.atlas', Laya.Handle.create(this, function(cow) {
    const anim = new Laya.Animation();
    anim.loadAtlas('res/atlas/cow.atlas');
    anim.interval = 200; // 帧动画间隔
    anim.play();
}))
```

### 物理引擎与碰撞关系
```js
// 设置重力值 为0 
Laya.Physics.I.gravity = [x: 0, y: 0]
```
tips: 物体碰撞集合mesk 按位与 其他物体的category 为1 则 两物体可发生碰撞，而不是直接穿过


### 动画编辑器使用
> laya 中动画是独立的场景，可新建动画，然后利用laya 动画编辑器编辑关键帧形成动画，编辑好的动画可当作节点在场景中使用。