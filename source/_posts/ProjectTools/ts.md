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

### 联合类型
```js
let val: string|number 
val = 12 
console.log("数字为 "+ val) 
val = "Runoob" 
console.log("字符串为 " + val)
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
  [propName: string]: any; // 其他未知的属性
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

// 构造函数
interface Point {
  new (x: number, y: number): Point;
  x: number;
  y: number;
}
class Point2D implements Point {
  readonly x: number;
  readonly y: number;

  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
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

### 泛型
```js
// 类型变量 T
function loggingIdentity<T>(arg: T): T {
  console.log(arg.length); // Error T doesn't have .length
  return arg;
}

// 约束型类型变量
interface Lengthwise {
  length: number
}
function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length); // Now we know it has a ,length property, so no more error
  return arg;
}

```

### 泛型与联合类型高级用法
```js
interface Foo {
  name: string;
  sex: Boolean;
  age: number
}

// keyof 操作符是在 TypeScript 2.1 版本引入的，该操作符可以用于获取某种类型的所有键，其返回类型是联合类型
type T =  keyof Foo
type Keys = "name" | "sex";


type Obj = {
  // in 操作符用于遍历目标类型的公开属性名。类似for ...in
  [p in Keys]: p extends T ? Foo[p] : never
}

const obj: Obj = {
  name: 'egg',
  sex: true,
  age: 520, // age does not exist in type Obj
}

// typeof 用于获取目标变量的类型
const objOne: typeof obj = {
  name: 'yeg',
  sex: false,
}

// infer 表示在 extends 条件语句中待推断的类型变量
// 在下面的第一条类型语句中 infer P 表示待推断的函数参数, 如果 T 能赋值给 (arg: infer P) => any，则结果是 (arg: infer P) => any 类型中的参数 P，否则返回为 T。
/**
 * Obtain the parameters of a function type in a tuple
 */
type Parameters<T extends (...args: any) => any> = T extends (...args: infer P) => any ? P : never;

/**
 * Obtain the return type of a function type
 */
type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any;

// 封装
type Pick<T, k extends keyof T> = {
  [p in k]: T[p]
}

type Exclude<T, U> = T extends U ? never : T;

type Omit<T, k extends string | number | symbol> = {
  [p in Exclude<keyof T, k>]: T[p]
}

type Partial<T> = {
  [p in keyof T]?: T[p]
}

type Required<T> = {
  [p in keyof T]-?: T[p]
}

type Readonly<T> = {
  readonly [p in keyof T]: T[p]
}

type Record<K extends string | number | symbol, T> = {
  [p in K]: T
}
// 更多请看源码

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