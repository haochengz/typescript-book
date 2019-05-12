# 对象的类型 - 接口

在Typescript中对象的类型是由接口定义的.

## 什么是接口

接口在面向对象中是一个重要的概率, 它对对象的行为进行了抽象. 对象实现接口所约定的行为.

```ts
interface Person {
  name: string;
  age: number;
}

// 变量me是一个Person
let me: Person = {
  name: 'Harris Thompson',
  age: 45
}

// 错误! 属性不能比接口所约定的少
let he: Person = {
  name: 'Toyotomi Hideyoshi'
}

// 错误! 属性不能比接口所约定的多
let she: Person = {
  name: 'Екатерина II Алексеевна'
  age: 257,
  knownAs: 'Catherine the Great'
}
```

## 可选属性

在接口中可以定义部分可选属性, 对象在实现的时候可以实现或不实现.

```ts
interface Person {
  name: string;
  age?: number;
}

// 此时age属性是可选的
let me: Person = {
  name: 'James Bond'
}

// 错误! 依然不能包含接口中未定义的属性
let mike: Person = {
  name: 'Mike Bolton',
  age: 44,
  isTarget: true
}
```

## 任意属性

如果希望对象在实现一个接口时可以包含任意类型的属性:

```ts
interface Person {
  name: string;
  age?: number;
  [propName: string]: any
}

// 此时的isTarget属性作为任意属性是可以的
let mike: Person = {
  name: 'Mike Bolton',
  age: 44,
  isTarget: true,
  
  // 任意属性的数量也是任意的
  isDead: false
}
```

*然而需要注意的是一旦定义了任意属性, 那么所有其他属性的类型都必须是任意属性类型的子类型*

```ts
interface Person {
  name: string;
  age?: number;
  [propName: string]: string;
}

// 错误! age的类型不是任意类型的子类型
let mike: Person = {
  name: 'Mike Bolton',
  age: 44,
  isTarget: true,
  isDead: false
}
```

## 只读属性

在接口中定义了只读属性后, 所有实现了该接口的对象只能一次性初始化只读属性的值, 不能对其从新赋值.

```ts
interface Person {
  readonly id: number;
  name: string;
  age?: number;
  [propName: string]: any;
}

let mike: Person = {
  id: 780001,
  name: 'Mike Bolton',
  age: 44,
  isTarget: true,
  isDead: false
}

// 可以修改非只读属性
mike.isTarget = false;

// 错误! 不能修改只读属性
mike.id = 790001;
```

