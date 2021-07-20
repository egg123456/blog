---
title: ts
date: 2018/5/11
categories:
- ProjectTools
---

# ts

### get start 
1. npm install -g typescript
2. create demo.ts file
```js
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.innerHTML = greeter(user);
```
3. tsc ./demo.ts

### base type
```js
// 布尔
let isDone: boolean = false;

// 数字
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;

// 字符串
let name: string = "bob";
name = "smith";

// 数组
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];

// 元组 类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ['hello', 10]; // OK
// Initialize it incorrectly
x = [10, 'hello']; // Error

// 枚举
enum Color {Red, Green, Blue}
let c: Color = Color.Green;

// 任意值
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean

// 空值
function warnUser(): void {
    alert("This is my warning message");
}

// null and undefined
let u: undefined = undefined;
let n: null = null;
// 默认情况下null和undefined是所有类型的子类型。 就是说你可以把null和undefined赋值给number类型的变量。

```

### 类型断言
通过类型断言这种方式可以告诉编译器，“相信我，我知道自己在干什么”。
```js
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
// let someValue: any = "this is a string";
// let strLength: number = (someValue as string).length;
```

### ts 支持 es6 的解构与展开
```js
// 解构
let {a, b}: {a: string, b: number} = o;
// 展开
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { food: "rich", ...defaults };
```

### 接口
```js
// 对象
interface SquareConfig {
  color: string; // 必须的
  width?: number; // 可有可无的
  readonly y: number; // 只读的
}
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a; // 只读数组 只是把数组所有可变方法去掉了

// 函数类型的接口
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(src: string, sub: string): boolean {
  let result = src.search(sub);
  return result > -1;
}

// 可索引类型
interface StringArray {
  readonly [index: number]: string; // 索引只读 禁止给索引赋值 如 myArray[0] = 'egg'
}
let myArray: StringArray;
myArray = ["Bob", "Fred"];
let myStr: string = myArray[0];

// 类类型
interface ClockInterface {
  currentTime: Date;
  setTime(d: Date);
}
class Clock implements ClockInterface {
  currentTime: Date;
  setTime(d: Date) {
      this.currentTime = d;
  }
  constructor(h: number, m: number) { }
}

```

### config
```json
// tsconfig.json
{
  "compilerOptions": {
    "module": "system",
    "noImplicitAny": true,
    "removeComments": true,
    "preserveConstEnums": true,
    "outFile": "../../built/local/tsc.js",
    "sourceMap": true
  },
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules",
    "**/*.spec.ts"
  ]
}
```