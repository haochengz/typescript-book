# 内置对象

ECMA标准提供了以下的内置对象:

`Boolean`  | `Error` |  `Date` | `RegExp` | `Document` | `HTMLElement` | `Event` | `NodeList`, 等等. 在Typescript中可以直接将变量定义为这些类型. 还有更多[内置对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects). 在Typescript中这些内置对象的定义可以在[Typescript核心库的定义文件](https://github.com/Microsoft/TypeScript/tree/master/src/lib)中找到.

## Typescript 核心库的定义文件

[Typescript核心库的定义文件](https://github.com/Microsoft/TypeScript/tree/master/src/lib)定义了所有浏览器环境需要用到的类型, 相当于预置在了Typescript中. 当使用一些常用方法时, Typescript就可以自动的做出类型约束了.

```ts
// 错误! 类型错误, pow方法只接受number类型的参数
Math.pow(10, '2');

// 在核心库中的某处, 这个方法的类型被定义为:
interface Math {
    /**
     * Returns the value of a base expression taken to a specified power.
     * @param x The base value of the expression.
     * @param y The exponent value of the expression.
     */
    pow(x: number, y: number): number;
}
```

*Typescript核心库的定义中并不包括Node.js中的内置对象和方法*

如果需要用TypeScript写Node.js, 就可以引入第三方的Node.js声明文件:

> nom install @types/node —save-dev

