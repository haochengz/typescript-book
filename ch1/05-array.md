# 数组的类型

## 类型 + 方括号表示数组

Typescript中数组有多重定义的方法, 其中最简单的是类型 + 方括号的表示法:

```ts
let fibbonacci: number[] = [0, 1, 1, 2, 3, 5, 8];

// 错误! fibbonacci是数值类型的数组, 不能包含其他类型的值
let fibbonacci: number[] = [0, 1, '1', 2, 3, 5, 8];

// 错误! 数组的方法也会根据类型对值进行约束
fibbonacci.push('13')

// 使用联合类型使数组元素可以是多种类型
const fibbonacci1: (string | number)[] = [
  0, 1, '1', 2, 3, 5, 8
]

//如果直接赋值, 该类型被推导为联合类型
// (number: string)[]
let fibbonacci = [
  0, 1, 1, '2', 3, 5, 8
];
```

## 数组泛型

```ts
// fibbonacci的类型是number[]
let fibbonacci: Array<number> = [
  0, 1, 1, 2, 3, 5, 8
];

// 泛型同样支持联合类型
const fibbonacci2: Array<number | string> = [
  0, 1, '1', 2, 3, 5, 8
];
```

## 使用接口表示数组

```ts
interface NumberArray {
  [index: number]: number;
}

let fibbonacci: NumberArray = [
  0, 1, 1, 2, 3, 5, 8
];
```

## Any类型在数组中的应用

```ts
// 必须是数组, 但数组中的元素不做类型约束
let ls: any[] = [
  'Mike', 22, {
    City: 'Macau',
    website: 'www.macau.gov'
  }
]

// 不做类型约束
let ls: any = [
  'Boo', 22, {
    City: 'Macau',
    website: 'www.macau.gov'
  }
]
```

## 类数组

类数组(Array-like Object)是一种特殊的类, 如用于表示函数参数的arguments变量. 类数组和数组一样可以使用数字索引访问其中元素, 但是不能迭代遍历.

```ts
function sum() {
  
  // 错误! 类数组不是数组
  let args: number[] = arguments;
}

function sum() {
  
  // 常见的类数组都有自己的接口定义
  let args: IArguments = arguments;
}
```

