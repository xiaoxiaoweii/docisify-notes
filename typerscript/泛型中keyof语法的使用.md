# 泛型中keyof语法的使用

## 用途

在Ts中使用类,类中有对象,根据对象的index返回相应的内容,推断正确返回内容的类型时可以使用keyof做到。

## 写法

```typerscript
interface Person {
  name: string;
  age: number;
  gender: string;
}

/*  
type T = 'name';
key: 'name';
Person['name']

type T = 'age';
key: 'age';
Person['age']

type T = 'gender';
key: 'gender';
Person['gender']
*/


class Teacher {
  constructor(private info: Person) {}
  getInfo<T extends keyof Person>(key: T): Person[T] {
  return this.info[key];
  }
}

const teacher = new Teacher({
  name: 'xiaoxiaoweii',
  age: 100,
  gender: 'male',
});

/* 强制返回为string类型 不是最优写法 
const test = teacher.getInfo('name') as string;
console.log(test);
*/
const test1 = teacher.getInfo('name');
const test2 = teacher.getInfo('age');
const test3 = teacher.getInfo('gender');
console.log(test1,test2,test3);

```
