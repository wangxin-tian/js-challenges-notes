# JS

## 浅拷贝

```js
let shawdowClone = function (source) {
    let target = Array.isArray(source) ? [] : {};
    for (let item in source) {
        target[item] = source[item];
    }

    return target;
}
```

## 深拷贝

```js
/* 1. JSON 深拷贝 缺点：无法保存特殊对象 */
let source = {};
let target = JSON.parse(JSON.stringify(source));
```

```js
/* 2. 递归深拷贝 */
/*缺陷当实现循环自我引用时报错*/
let deepClone = function (source) {
    if (source === null || typeof source !== "object" || source instanceof Date || source instanceof RegExp) {
        return /*递归需要设置出口*/ source;
    }

    let target = Array.isArray(source) ? [] : {};
    for (let item in source) {
        if (source.hasOwnProperty(item)) {
            target[item] = deepClone(source[item]);
        }
    }

    return target;
}
```

## 类型检查

```js
/// 类型检查
let checkType = function (type) {
    return function (obj) {
        let theType = `[object ${type}]` === Object.prototype.toString.call(obj) ? true : false;
        console.log(Object.prototype.toString.call(obj));
        console.log(`[object ${type}]`);
        return theType;
    }
}
// let isArray = checkType("Array");
// let arr = [];

// console.log(isArray(arr));
```

## 防抖函数

```js
/// 防抖函数
let debounce = function (delay, callback) {
    let timer;
    return function (value) {
        clearTimeout(timer); /*通过闭包存储计时器*/
        timer = setTimeout(function () {
            callback(value);
        }, delay);
    }
}
```

## 节流函数

```js
/// 节流函数
/*1. 计时器实现*/
let throttle = function (wait, callback) {
    let timeout; /* timeout有值的时候不执行 */
    return function () {
        if (!timeout) {
            timeout = setTimeout(function () {
                callback.call(...arguments);
                timeout = null;
            }, wait);
        }
    }
}
```

```js
/*2. Date实现*/
function throttle(fn, delay) {
    var previous = 0; //new Date()
    return function () {
        var _this = this;
        var args = arguments;
        var now = new Date();
        if (now - previous > delay) {
            console.log("_this: ", _this);
            fn.apply(_this, args);
            previous = now;
        }
    }
}
```
