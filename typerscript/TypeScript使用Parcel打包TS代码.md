# TypeScript 使用 Parcel 打包 TS 代码

> 初始化 package.json

```shell
  npm init -y
```

> 初始化 tsconfig.json

```shell
  tsc --init
```

> 安装 parcel | [github 地址](https://github.com/parcel-bundler/parcel)

```shell
  npm install parcel@next -D
```

> tsconfig.json 相关配置

```json
  "outDir": "./dist", //输出路径
  "rootDir": "./src", // 根路径
```

> package.json 配置快捷命令

```json
"scripts": {
　　"test": "parcel ./src/index.html"
}
```

> index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <!-- 直接引入ts文件相对路径 打包自动转为js文件 -->
    <script src="./demo.ts"></script>
  </body>
</html>
```

> demo.ts 文件测试

```typescript
const Person: string = 'xiaoxiaoweii';
console.log(Person);
```

> 测试

```shell
npm run test
```
