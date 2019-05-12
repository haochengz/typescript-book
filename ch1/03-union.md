# 联合类型

联合类型(Union)表示一个变量的取值可以是一组类型中的任意一种.

```ts
let num: string | number;

// 变量num的值既可以是string, 也可以是number
num = 7;
num = 'hello';

// 但不能是除string或number外的其他类型
num = true;
```

## 访问联合类型的属性或方法

但Typescript不确定一个联合类型的变量当前值是什么类型时就只能访问所有可能类型中共有的属性或方法.

```ts
function getLength(seq: string | number): number {
  
  // 错误! seq变量未赋值的情况下无法得知其确切类型
  // 因此length属性无法访问
  return seq.length;
}

function getString(seq: string | number): string {
  
  // 不论string或number都有toString()方法
  // 因此这个访问是合法的
  return seq.toString();
}
```

联合类型的变量在被赋值时, 类型推导会为其推导出一个类型.

```ts
let num: string | number;

// 每次赋值num的类型都会相应的改变
num = 'seven';
num = 7;
```

