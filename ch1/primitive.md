
# 原始数据类型

在Javascript中的类型分为原始数据类型(Primitive data types)和对象类型(Object types)两种. 在Typescript中也是如此. 其中原始数据类型是指一些简单的类型. 包括了:

* 布尔类型

* 数值类型

* 字符串类型

* null

* undefined

* Symbol (ES6标准新加入的类型)

## 布尔类型

布尔类型仅有两个值, 即true和false, 在Typescript中使用 `boolean` 作为它的类型标识符:

```js
// 定义了一个布尔类型的变量
let isOk: boolean = true;

// Boolean是构造函数, 不是布尔类型, 因此以下代码将抛出错误
let isDone: boolean = new Boolean(1);
```

## 数值类型

在Javascript中没有浮点类型和整数类型的区分, 所有数字都属于数值类型, 数值类型可以包含以下的一些值:

```js
// 使用十进制表示的整数
let decimal: number = 6;

// 浮点数字的表示
let float: number = 6.66;

// 十六进制表示的整数
let hexdecimal: number = 0xff1;

// 二进制表示的整数
let binary: number = 0b100010;

// 八进制表示的整数
let octal: number = 0o100;

// 运算发生了未定义的结果时会得到这个特殊的值
// 如: 0/0 => NaN, NaN不和任何值相等, 包括它本身
let notANumber: number = NaN;

// 当一个浮点数查过了Javascript所能表示的最大值是将得到这个值
let infinityNumber: number = Infinity;
```

## 字符串类型

```js
let name: string = 'Tom';
let age: number = 22;

// 使用ES6中的模板字符串
let greeting: string = `Hi, this is ${name}. I'm ${age} years old.`;
```

## 空值(void)

在Javascript中没有void, 但在Typescript中可以使用void做为函数的返回类型表示不返回任何值.

```js
function sayHello(name:string): void {
  console.log(`Hello ${name}!`);
}

sayHello('world');
```

## null 和 undefined

null类型只有一个值即null, 如果一个变量的值为null, 该变量的值不是一个有效的对象, 数值, 字符串等. 处于向前兼容的原因, 使用`typeof null`将得到`object`. 因此null通常看做object类型的特殊值, 表示为空对象.

undefined类型也只有一个值即undefined. 用于表示未定义的数据, 定以后未赋值的数据和不存在的属性.

null和undefined是所有类型的子类型, 也就是这两个值可以赋值给任意类型的变量.
