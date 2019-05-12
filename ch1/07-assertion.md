# 类型断言

类型断言指手动的指定一个值得类型, 仅适用于联合类型.

当Typescript不确定一个联合类型的变量的当前具体类型时, 只能访问到联合类型里所有类型的共有属性或方法. 而当需要使用非共有方法时就需要通过类型断言将该变量的类型断言为一个具体的类型.

```ts
function getLen(seq: string | number): number {
  if((<string>seq).length) {
    return (<string>seq).length;
  } else {
    return seq.toString().length;
  }
}
```

在变量之前加上 `<TypeName>` 即可. 类型断言不是类型转换, 只能断言为联合类型中的类型.

```ts
// 另外一种方式, (var as TypeName)
// tsx语法, 即React中的Typescript只支持这种写法
function getLen(seq: string | number): number {
  if((seq as string).length) {
    return (seq as string).length;
  } else {
    return seq.toString().length;
  }
}
```

