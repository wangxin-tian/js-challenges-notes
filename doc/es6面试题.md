# 面试题

## var、let、const之间的区别

围绕下面五点展开：

- 变量提升
- 暂时性死区
- 块级作用域
- 重复声明
- 修改声明的变量
- 使用

## 扩展

### 数组

扩展符
`Array.from` 类数组转数组
`Array.of` 一组值转数组
`copyWithin`
`find` 找出第一个符合条件的数组成员
`findIndex` 返回第一个符合条件的数组成员的位置
`fill`
`entries`
`keys`
`values`
`includes`
`flat` 数组扁平化
`flatMap`

### 对象

属性名表达式 `[计算属性名]`
super关键字 用于指向原型对象
遍历 遵循：数字-升序、字符-时间、符号-时间
`Object.is()`
`Object.assign()`
`Object.getOwnPropertyDescriptors()`
`Object.setPrototypeOf()`
`Object.getPrototypeOf()`
`Object.keys()`
`Object.values()`
`Object.entries()`
`Object.fromEntries()`

### 函数

参数设置默认值，且不能再次声明
name属性和length属性
严格模式 `'use strict';` 只要函数中使用默认值、解构赋值、或扩展运算符，那么函数就会在严格模式下报错
箭头函数，拿到定义时所在的对象、无法作为构造函数、不能够使用arguments、无法作为生成器函数

## set、map理解

set集合
`add()`
`delete()`
`has()`
`clear()`

map字典
`size`属性返回成员总数
`set()`
`get()`
`has()`
`delete()`
`clear()`
遍历顺序是插入顺序

WeakSet和Weakmap
无法遍历
没有size
Weakset的成员必须是引用类型
WeakMap只接收对象作为键

## Promise使用场景

期约或承若
三种状态：pending、fulfilled、rejected
实例方法：then(),catch(),finally()
构造函数方法：all(),race(),allSettled(),resolve(),reject(),try()

race设置超时拒绝期约与请求期约，来处理请求超时
地狱回调改链式调用

## Generator使用场景

执行generator返回一个遍历器对象，可以依次遍历generator函数内部的每一个状态
使用yield表达式定义不同的内部状态
Symbol.iterator属性
yield暂停 next恢复

异步任务同步化

async/await将生成器语义增强，简化形式
区别是，generator还有迭代控制的功能

## Proxy使用场景

定义： 用于定义基本操作的自定义行为

```js
var proxy = new Proxy(target, handler)
```

target: 拦截对象
handler: 拦截行为 get set has deleteProperty ownKeys getOwnPropertyDescriptor defineProperty preventExtensions getPrototypeOf isExtendible setPrototypeOf apply construct
set() 严格模式下，set代理如果没有返回true，就会报错
deleteProperty() 方法用于拦截delete操作
取消代理 Proxy.revocable(target, handler);

Reflect 反射，用于在proxy的内部调用对象的默认行为

使用场景：设计模式中的代理模式
拦截、降低函数或类复杂度、校验

## 理解es6模块化

CommonJs： 早期node动态导入
es6： 静态导入 export import as ,
  也可以动态加载 import().then()

## 理解ES6中Decorator

类比装饰者模式：装饰者模式就是一种在不改变原类和使用继承的情况下，动态地扩展对象功能的设计理论。

优点：

- 代码可读性变强了，装饰器命名相当于一个注释
- 在不改变原有代码情况下，对原来功能进行扩展

修饰对象分为两种：

- 类的装饰，接收目标类；若想传递其他参数，需要在外层封装一层函数
- 类属性的装饰，此时接收原型对象、装饰的属性、装饰属性的描述对象

## core-decorators.js装饰器库
