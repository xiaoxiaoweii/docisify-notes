# Promise-区别实例对象与函数对象

## 区别实例对象与函数对象

- new 函数产生的对象 ------实例对象 | 对象
- 将函数作为对象使用 -----函数对象

```javascript
function Person () {}
const person = new Person() // Person构造函数 person是实例对象(对象)
console.log(Person.prototype) // 此时Person为函数对象
Person.bind({}) // 调用Person函数对象的bind方法
Person.call({}) // 调用Person函数对象的call方法
```

> 函数对象为. 则为函数对象 ()则为函数
