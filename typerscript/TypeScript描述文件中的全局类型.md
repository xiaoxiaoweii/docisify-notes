# TypeScript 描述文件中的全局类型

## 问题描述

在 Ts 文件中直接使用 jQuery 时,虽然打包以后的代码可以正常运行。不过由于 Ts 不能正常识别 js 中引用的库,会报错提示

```
Cannot find name '$'. Do you need to install type definitions for jQuery? Try `npm i @types/jquery`。
```

## 解决方式

### 安装其他人写好的文件

需要让 Ts 识别 js 安装的库 解决方法有两种

### 自己写.d.ts 文件

- 直接安装其他人写好的@types/jquery

```shell
  npm install --save-dev @types/jquery
```

- 自己写.d.ts

> d.ts 大名叫 TypeScript Declaration File，存放一些声明，类似于 C/C++的.h 头文件

#### .d.ts 内容

```typerscript
// 定义全局变量
/* declare var $: (param: () => void) => void; */

// 定义全局函数 一个函数多种形式 重载
interface JqueryInstance {
  html: (html: string) => JqueryInstance;
}

// 函数重载
declare function $(readyFunc: () => void): void;
declare function $(selector: string): JqueryInstance;

// 使用interface实现函数重载
/* interface JQuery {
  (readyFunc: () => void): void;
  (selector: string): JqueryInstance;
}

declare var $: JQuery; */

// 对对象进行类型定义 类惊进行类型定义 命名空间的嵌套
declare namespace $ {
  namespace fn {
    class init {}
  }
}
```
