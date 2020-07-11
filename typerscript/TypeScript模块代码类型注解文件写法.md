# TypeScript 模块代码类型注解文件写法

## 使用 module 的方式引入 jQuery

```shell
  cnpm install jquery --save
```

> 不以 cdn 的方式引入，而是以模块化的方式引入 jquery

## jquery.d.ts 写法

导入 module 'jquery', module 中进行定义

```typerscript
/* ES6 模块化 */

declare module 'jQuery' {
  interface JqueryInstance {
    html: (html: string) => JqueryInstance;
  }
  // 混合类型
  function $(readyFunc: () => void): void;
  function $(selector: string): JqueryInstance;
  namespace $ {
    namespace fn {
      class init {}
    }
  }
  // 导出$
  export = $;
}
```

## page.ts使用

```typerscript
/* $(function () {
  alert(123);
});
 */
import $ from 'jQuery'

$(function () {
  $('body').html('<div>123</div>');
  new $.fn.init();
});

```
