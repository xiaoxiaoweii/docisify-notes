# Promise-JS 的 error 处理

- [MDN error](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Error)

## 错误的类型

常见的内置错误

- Error : 所有错误的父类型

- ReferenceError: 引用的变量不存在

```javascript
console.log(a) // Uncaught ReferenceError: a is not defined
```

- TypeError: 数据类型不正确的错误

```javascript
let b = null
console.log(b.aaa) //Uncaught TypeError: Cannot read property 'aaa' of null
let a
console.log(a.aaa) //Uncaught TypeError: Cannot read property 'aaa' of undefined
let c = {}
c.aaa() // Uncaught TypeError: c.aaa is not a function
```

- RangeError: 数据值不在其所允许的范围内

```javascript
function fn () {
  fn()
}
fn() // js的error错误处理.html:24 Uncaught RangeError: Maximum call stack size exceeded
```

- SyntaxError: 语法错误

```javascript
const a = """" //Uncaught SyntaxError: Unexpected string
```

## 错误处理

- 捕获错误: try ... catch

```javascript
try {
  let b
  console.log(b.aaa)
} catch (error) {
  console.log(error) // TypeError: Cannot read property 'aaa' of undefined
  console.log(error.message) // Cannot read property 'aaa' of undefined
  console.log(error.stack) // TypeError: Cannot read property 'aaa' of undefined
}
console.log('出错之后')
```

- 抛出错误: throw error

```javascript
function something () {
  if (Date.now() % 2 === 1) {
    console.log('当前时间为奇数 可以执行任务')
  } else {
    throw new Error('当前时间为偶数 无法执行任务')
  }
}
try {
  something()
} catch (error) {
  alert(error.message)
}
```