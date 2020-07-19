# Promise-两种回调函数

## 同步回调

- 立即执行 完全执行完了才结束,不会放入回调队列中

```javascript
const arr = [1, 3, 5]
arr.forEach(i => {
  // 遍历的回调
  console.log(i)
})
console.log('forEach()之后')
```

## 异步回调

- 不会立即执行 会放入回调队列中将来执行

```javascript
setTimeout(() => {
  // 放入队列 将来执行
  console.log('timeout callback()')
}, 0)
console.log('setTimeout()之后')
```
