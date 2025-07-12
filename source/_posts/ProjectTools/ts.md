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

// 提取数组元素类型
type TYPE2<T> = T extends Array<infer U> ? U : T;
type A = TYPE2<string>; // string
type B = TYPE2<string[]>; // string
type C = TYPE2<(string | number)[]>; // string | number

// 提取对象属性类型
type PropertyType<T> = T extends { id: infer U, name: infer R } ? [U, R] : T;
type User = { id: number; name: string; };
type UserProperties = PropertyType<User>; // [number, string]

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

### .d.ts and .ts
#### 用途和功能
1. .ts文件‌：

+ 用途‌：.ts文件是TypeScript的源代码文件，包含实际的可执行代码和类型注解。这些文件会被TypeScript编译器编译成JavaScript，然后在支持JavaScript的环境中运行。
+ ‌功能‌：.ts文件可以包含函数、类、接口、类型别名、变量声明等所有TypeScript的语法结构‌12。

2. .d.ts文件‌：

+ 用途‌：.d.ts文件是TypeScript的声明文件，专门用来定义类型信息，不包含任何可执行代码。这些文件提供类型信息，帮助TypeScript编译器理解没有类型信息的代码库（如纯JavaScript库）的结构。
+ 功能‌：.d.ts文件通常包含类型声明，如接口、类型别名、命名空间、模块声明等，但不会包含实现细节。它们不会被编译器编译成JavaScript，而是用于静态类型检查和编辑器的智能感知（如自动补全、跳转到定义等）‌12。

#### 使用场景
+ ‌.ts文件‌：主要用于编写实际的程序代码，包含可执行逻辑和类型注解。
+ ‌.d.ts文件‌：主要用于为没有类型信息的代码库（如纯JavaScript库）提供类型信息，以便在TypeScript环境中进行静态类型检查和智能提示。

### interface和type
#### 定义范围‌
‌interface‌：主要用于描述对象类型，定义了具有相似名称和类型的对象结构。它可以定义方法和事件，适用于面向对象编程中的抽象定义‌12。
‌type‌：不仅可以表示对象类型，还可以表示基础类型（如string、number）、联合类型（如Dog | Cat）、元组类型等，具有更高的灵活性‌12。

#### ‌扩展性‌：
‌interface‌：可以通过extends和implements关键字扩展多个接口或类，适合于需要继承和多态的场景‌23。
‌type‌：虽然没有直接的扩展功能，但可以通过交叉类型（&）来实现成员类型的合并，适用于需要组合多个类型的场景‌24。

#### 合并声明‌：
‌interface‌：如果声明两个同名的interface，它们会合并声明，新增的成员会被添加到原有的接口中‌24。
‌type‌：如果声明两个同名的type，会导致编译错误，因为TypeScript不允许重复声明相同的类型别名‌4。

#### ‌使用场景‌：
‌interface‌：更适合用于面向对象编程中的抽象定义，可以强制实现类具有特定的属性和方法，适用于需要明确对象结构和行为的场景‌
