---
title: ES新特性
date: 2024-10-17
categories: ["JavaScript",ES]
---
ES6（也叫ECMAScript 2015）及后续版本（ES7、ES8、ES9 等）为 JavaScript 带来了大量的新特性，极大地增强了语言的能力、可读性和开发体验。下面我将详细总结从 **ES6** 到 **最新版本（截至2024年）** 的新特性，并对其逐一解释。

## 1. **ES6 (ECMAScript 2015) 新特性**

### 1.1 `let` 和 `const`
- **`let`**：块级作用域变量，声明的变量只在其所在的块内有效。
- **`const`**：常量，用于声明不会被重新赋值的变量。

**示例**：
```javascript
let a = 10;
const b = 20;
```

### 1.2 箭头函数
- 箭头函数是一种简写函数表达式，并且不会绑定自己的 `this`， `arguments`， `super` 或 `new.target`，它使用的是父级作用域中的 `this` 值。

**示例**：
```javascript
const add = (x, y) => x + y;
```

### 1.3 模板字面量（Template Literals）
- 允许使用反引号（`` ` ``）来定义多行字符串，支持嵌入变量和表达式。

**示例**：
```javascript
const name = 'John';
console.log(`Hello, ${name}!`);  // 输出: Hello, John!
```

### 1.4 解构赋值
- 允许从数组或对象中提取数据，赋值给变量。

**示例**：
```javascript
let [a, b] = [1, 2];
let {name, age} = {name: 'John', age: 30};
```

### 1.5 扩展运算符和剩余参数（Spread/Rest Operator）
- **扩展运算符**：可以在函数调用时展开数组或对象。
- **剩余参数**：在函数中收集所有其余参数。

**示例**：
```javascript
let arr = [1, 2, 3];
console.log(...arr);  // 展开: 1 2 3

function sum(...args) {
    return args.reduce((a, b) => a + b, 0);
}
```

### 1.6 类（Classes）
- ES6 引入了类的概念，提供了基于 `class` 关键字的语法糖，简化了原型继承的操作。

**示例**：
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }
}
```

### 1.7 模块（Modules）
- 使用 `import` 和 `export` 关键字来引入和导出模块，支持模块化开发。

**示例**：
```javascript
// 导出
export const PI = 3.14;

// 导入
import { PI } from './math.js';
```

### 1.8 Promise
- 引入 `Promise` 对象，用于处理异步操作，避免回调地狱。

**示例**：
```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("Done"), 1000);
});

promise.then(result => console.log(result));
```

### 1.9 Symbol
- `Symbol` 是一种新的原始数据类型，表示独一无二的值，通常用于对象属性的标识符。

**示例**：
```javascript
let sym = Symbol("unique");
```

### 1.10 for...of 循环
- `for...of` 循环用于遍历可迭代对象（如数组、字符串等）。

**示例**：
```javascript
let arr = [1, 2, 3];
for (let val of arr) {
    console.log(val);
}
```

### 1.11 Set 和 Map
- **Set**：一种新的数据结构，类似数组，但成员值唯一。
- **Map**：键值对集合，类似对象，但键可以是任意数据类型。

**示例**：
```javascript
let set = new Set([1, 2, 3]);
let map = new Map([["key", "value"]]);
```

## 2. **ES7 (ECMAScript 2016) 新特性**

### 2.1 指数运算符
- 引入 `**` 作为指数运算符，代替 `Math.pow`。

**示例**：
```javascript
console.log(2 ** 3);  // 输出: 8
```

### 2.2 `Array.prototype.includes`
- `includes` 方法用于检查数组中是否包含某个值。

**示例**：
```javascript
let arr = [1, 2, 3];
console.log(arr.includes(2));  // 输出: true
```

## 3. **ES8 (ECMAScript 2017) 新特性**

### 3.1 异步函数（Async/Await）
- `async/await` 是 `Promise` 的语法糖，使得异步代码可以用同步的方式书写。

**示例**：
```javascript
async function fetchData() {
    let response = await fetch('https://api.example.com/data');
    let data = await response.json();
    return data;
}
```

### 3.2 `Object.values` 和 `Object.entries`
- `Object.values` 返回对象的所有值。
- `Object.entries` 返回对象的键值对数组。

**示例**：
```javascript
let obj = {a: 1, b: 2};
console.log(Object.values(obj));  // 输出: [1, 2]
console.log(Object.entries(obj)); // 输出: [["a", 1], ["b", 2]]
```

### 3.3 字符串填充方法
- `padStart` 和 `padEnd` 方法用于在字符串的开头或结尾填充指定的字符。

**示例**：
```javascript
console.log('5'.padStart(3, '0')); // 输出: "005"
```

## 4. **ES9 (ECMAScript 2018) 新特性**

### 4.1 对象扩展运算符
- 引入对象的扩展运算符，允许浅拷贝对象。

**示例**：
```javascript
let obj1 = {a: 1, b: 2};
let obj2 = {...obj1, c: 3};  // 输出: {a: 1, b: 2, c: 3}
```

### 4.2 异步迭代（`for await...of`）
- 允许在异步可迭代对象上使用 `for await...of` 语法。

**示例**：
```javascript
async function process(data) {
    for await (let item of data) {
        console.log(item);
    }
}
```

### 4.3 正则表达式改进
- 引入了 `dotAll` 模式 (`/s`)，使 `.` 能够匹配包括换行符在内的任何字符。

**示例**：
```javascript
let regex = /hello.world/s;
console.log(regex.test('hello\nworld'));  // 输出: true
```

## 5. **ES10 (ECMAScript 2019) 新特性**

### 5.1 `Array.prototype.flat` 和 `flatMap`
- `flat` 方法用于将嵌套数组“拉平”。
- `flatMap` 结合了 `map` 和 `flat` 的功能。

**示例**：
```javascript
let arr = [1, [2, [3]]];
console.log(arr.flat(2));  // 输出: [1, 2, 3]
```

### 5.2 `Object.fromEntries`
- 允许将键值对数组转换为对象。

**示例**：
```javascript
let entries = [['a', 1], ['b', 2]];
let obj = Object.fromEntries(entries);  // 输出: {a: 1, b: 2}
```

### 5.3 `String.prototype.trimStart` 和 `trimEnd`
- 用于去除字符串开头或结尾的空白字符。

**示例**：
```javascript
let str = '   Hello   ';
console.log(str.trimStart());  // 输出: 'Hello   '
```

## 6. **ES11 (ECMAScript 2020) 新特性**

### 6.1 可选链（Optional Chaining `?.`）
- 安全地访问嵌套对象的属性，避免抛出 `TypeError`。

**示例**：
```javascript
let user = {};
console.log(user?.address?.street);  // 输出: undefined
```

### 6.2 空值合并运算符（Nullish Coalescing `??`）
- 当左侧操作数为 `null` 或 `undefined` 时，返回右侧操作数。

**示例**：
```javascript
let val = null ?? 'default';
console.log(val);  // 输出: 'default

'
```

### 6.3 动态 `import`
- 支持动态导入模块，返回 `Promise`。

**示例**：
```javascript
import('module').then(module => {
    module.doSomething();
});
```

## 7. **ES12 (ECMAScript 2021) 新特性**

### 7.1 `String.prototype.replaceAll`
- 替换字符串中的所有匹配项。

**示例**：
```javascript
let str = 'aabbcc';
console.log(str.replaceAll('b', 'x'));  // 输出: 'aaxxcc'
```

### 7.2 逻辑赋值运算符
- 包括 `&&=`, `||=`, 和 `??=`

**示例**：
```javascript
let a = true;
a &&= false;  // a 变为 false
```

## 8. **ES13 (ECMAScript 2022) 新特性**

### 8.1 `Top-level await`
- 允许在模块的顶层使用 `await`。

**示例**：
```javascript
let data = await fetch('https://api.example.com');
console.log(await data.json());
```

### 8.2 类的静态块
- 静态块允许在类的静态上下文中执行代码。

**示例**：
```javascript
class C {
    static {
        // 静态初始化代码
    }
}
```

## 9. **ES14 (ECMAScript 2023) 新特性**

### 9.1 `Array.prototype.findLast` 和 `findLastIndex`
- 从数组末尾开始查找元素。

**示例**：
```javascript
let arr = [1, 2, 3, 4];
console.log(arr.findLast(x => x % 2 === 0));  // 输出: 4
```

### 9.2 哈希集合/哈希地图 `HashSet` 和 `HashMap`
- 引入了对哈希表的支持，更快的数据查找和管理操作。

---

以上是从 ES6 到最新版本（ES14）的重要新特性总结。每个版本都为 JavaScript 增添了功能，提升了语言的性能和开发者的使用体验。