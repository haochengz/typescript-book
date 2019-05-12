# 函数的类型

## 函数声明

在Javascript中有两种方式定义一个函数, 函数声明和函数表达式.

```js
function sum(x, y) {
  return x + y;
}

const sum = function(x, y) {
  return x + y;
}
```

在Typescript中将对函数的输入和输出进行约束.

```ts
function sum(x: number, y: number): number {
  return x + y;
}

sum(1, 3); //=> 4

// 错误不能像javascript一样省略或者多传参数
// 函数参数的数量和类型都受到约束
sum(1);
sum(1, 2, 3);
```

## 函数表达式

函数表达式是Javascript中定义函数的另外一种方法. 然而在Typescript中可能会发生一些混淆.

```ts
// 变量sum的类型是由类型推导得出的, 因为以下代码只定义了
// 等式右侧的匿名函数, 而不是等式左侧的sum变量
let sum = function(x: number, y: number): number {
  return x + y;
}

// 注意! => 符号并非ES6中的箭头函数, 而是指函数的返回
// 类型
let sum: (x: number, y: number) => number = 
    function(x: number, y: number): number {
    return x + y;
}
```

## 使用接口定义函数的形状

```ts
interface SearchFunc {
  (source: string, subString: string): boolean;
}

let search: SearchFunc;
search = function(source: string, subString: string) {
  return source.search(subString) !== -1;
}
```

## 可选参数

和Javascript不同, Typescript不允许参数个数和参数列表中定义的参数个数不同. 需要使用单独的语法约定可选的参数, 这个语法就是使用?符号明确的表示一个参数是可选的.

```ts
// 参数last是可选的, 可选参数必须在参数表后面, 可以有多个
// 可选参数后面只能有剩余参数
function getFullName(first: string, last?: string): string {
  if(last) {
    return first + ' ' + last;
  } else {
    return first;
  }
}

getFullName('Michael'); //=> Michael
getFullName('Michael', 'Jordan'); //=> Michael Jordan
```

## 默认参数值

默认参数值是ES6中的新增特性, Typescript中同样支持了.

```ts
function getFullName(first: string, last?: string = 'Jackson'): string {
  if(last) {
    return first + ' ' + last;
  } else {
    return first;
  }
}

getFullName('Michael'); //=> Michael Jackson
getFullName('Michael', 'Jordan'); //=> Michael Jordan

//----------

function getFullName(first: string = 'Tom', last?: string = 'Jackson'): string {
  if(last) {
    return first + ' ' + last;
  } else {
    return first;
  }
}

// 默认参数并不受必须在参数表后面的限制
getFullName(undefined, 'Jones'); //=> Tom Jones
getFullName('Michael Jordan'); //=> Michael Jordan
```

## 剩余参数

剩余参数同样是ES6中的新特性, Typescirpt中使用同样的方式取得剩余参数, 也可以约定剩余参数的类型.

```js
// 在Javascript中这样取得剩余参数, 在Typescript中同样适用
function push(array, ...items) {
  items.forEach(item => {
    array.push(item);
  })
}

let arr = [];
push(arr, 1, 2, 3, 4);
```

在Typescript中使用类型约束:

```ts
function push(array: any[], ...items: number[]) {
  items.forEach(function(item: number) {
    array.push(item);
  })
}

let arr = [];
push(arr, 1, 2, 3, 4);
```

剩余参数只能是最后一个参数, 且只能有一个.

## 函数重载

在其他编程语言中函数重载指调用时依据不同的参数列表调用不同的函数. 意味着可以具有多个同名函数, 通过参数表的不同区分这些同名函数. 在Javascript中由于灵活的参数传递规则, 可以手动实现类似函数重载的功能. 在Typescript利用联合类型对函数重载提供了在语言层面的支持.

```ts
function reverse(x: number | string): number | string  {
  if(typeof x === 'number') {
    return Number(x.toString().split('').reverse().join(''));
  } else if(typeof x === 'string') {
    return x.split('').reverse().join('');
  }
}

// 依据不同的参数传入类型执行了不同的代码块, 以及
// 输出不同类型的结果. 在Javascript中也可以这么
// 手动处理不同的入参类型
reverse(123); //=> 321
reverse('hello'); //=> 'olleh'
```

Typescript中支持了重载的声明多个reverse函数原型.

```ts
// 重复的声明了多次reverse函数, 最后一个是该函数的实现
// 调用时Typescript从上方开始匹配函数声明的原型, 将匹配
// 到的第一个函数原型作为调用函数的类型. 因此如果函数声明
// 中的类型有包含关系的话, 应该将更精确的原型放在前面.
function reverse(x: number): number;
function reverse(x: string): string;
function reverse(x: number | string): number | string  {
  if(typeof x === 'number') {
    return Number(x.toString().split('').reverse().join(''));
  } else if(typeof x === 'string') {
    return x.split('').reverse().join('');
  }
}
```

