# Promise 的理解和使用

## Promise 是什么

### 抽象表达

- Promise 是 JS 中进行异步编程的新的解决方案

### 具体表达

- 语法：Promise 是一个构造函数
- 功能：Promise 对象用来封装一个异步操作并可以获取其结果

### Promise 的状态改变

- pending 变为 resolved
- pending 变为 rejected

> 一个 promise 对象只能改变一次

## Promise 的基本使用

```javascript
const p = new Promise((resolve, reject) => {
  // 执行器函数
  // 执行异步操作任务
  setTimeout(() => {
    const time = Date.now() // 当前时间是偶数 成功 否则失败
    if (time % 2 == 0) {
      // 成功 调用resolve(value)
      resolve('成功的数据, time=' + time)
    } else {
      // 失败 调用reject(reason)
      resolve('失败的数据, time=' + time)
    }
  })
}, 1000)
p.then(
  value => {
    console.log('成功的回调', value)
  }, // 接收得到成功的数据 onResolved
  reason => {
    console.log('失败的回调', reason)
  } // 接收得到失败的value数据 onRejected
)
```

## 为什么使用 Promise

- 指定回调函数的方式更加灵活
  - 旧的必须在启动异步任务前指定
  - promise 启动异步任务 返回 promise 对象 给 promise 绑定回调函数
- 支持链式调用,解决回调地狱的问题
  - 回调函数嵌套调用,嵌套过深,不易阅读

### 使用纯回调函数

```javascript
createAudioFileAsync(audioSettings, successCallback, failureCallback)
```

### 使用 Promise

```javascript
const promise = createAudioFileAsync(audioSettings)
setTimeout(() => {
  promise.then(successCallback, failureCallback)
}, 3000)
```
