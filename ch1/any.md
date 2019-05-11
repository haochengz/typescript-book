
# 任意值类型

任意值(Any), 一个变量被声明为any类型后可以将任何类型的值赋值给它. 或者说Typescript不对any类型的变量做类型检查.

```js
let num: string = '7';

// 错误! 非any类型的变量只能被赋值为它声明时指定类型的值
num = 7;

let num: any = '7';

// any类型可以被赋值为任意类型的值
num = 7;
num = [1, 2, 3];
```

一个变量在声明时未指定其类型且未被赋予初始值则被认为是any类型.

```js
let num;

// 此时num是any类型
num = '7';
num = 7;
```
