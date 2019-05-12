# 声明文件

当使用第三方库时, 需要引入它的声明文件, 才能在编辑器中获得对应的代码补全, 接口提示等功能.

## 什么是声明语句

在使用第三库时, 如JQuery. 通过在html的script标签引入JQuery后就可以使用全局变量 `$`或`JQuery`了.

```js
// 这是Javascript代码
$('#foo');
// or
JQuery('#foo');
```

但对于Typescript而言需要进行类型约束, 因此tsc编译器必须知道`$`或`JQuery`的类型信息. 所以在使用之前需要首先引入其声明:

```ts
declare var JQuery: (selector: string) => any;

// 可以使用了
JQuery('#foo');
```

在以上的代码中并没有真正的定义`JQuery`变量, 只是声明了它的类型信息用于编译时的静态类型检查. 编译结果中并没有这样的声明语句.

## 什么是声明文件

按照惯例我们会将某个库的声明语句放到一个单独的文件中以便于调用者的引用. 如对于JQuery而言它的声明文件就是: [JQuery.d.ts](https://github.com/xcatliu/typescript-tutorial/tree/master/examples/declaration-files/03-jquery-d-ts). 声明文件必须以`.d.ts`结尾.

通常Typescript会解析项目中所有的`*.ts`或`*.tsx`文件, 其中也就包括了`*.d.ts`结尾的文件. 所以将声明文件放在项目中时, 其他所有文件都可以获得类型定义.

如果任然无法解析, 那么就需要检查`tsconfig.json`文件中的`files`, `include`和`exclude`配置了, 确保其中包含了声明文件.

### 第三方声明文件

社区中已经为我们提供大量的类型声明文件, 可以之间下载使用. 最好的方法时使用 `@types` 同意管理第三方库的声明文件. 已JQuery为例:

> npm install @types/jquery —save-dev

安装对应的声明模块即可, 可以在[这里](https://microsoft.github.io/TypeSearch/)看到大量的声明文件.