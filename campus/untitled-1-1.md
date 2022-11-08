# 实现 call/apply/bind/new

自己实现call apply bind new来理解这些函数的作用

这里用es6语法实现，只用es5语法实现可见 [https://github.com/mqyqingfeng/Blog/issues/11](https://github.com/mqyqingfeng/Blog/issues/11)

## call

### 简介

call指定了函数的this值和参数并调用函数

```javascript
fun.call(thisArg, arg1, arg2, ...);
```

### 实现

```javascript
function myCall(obj, ...args) {
    obj = obj || window; // call对象为null情况下指向window
    obj._fn = this; // 将函数设置为obj的属性
    let result = obj._fn(...args); // 调用函数，此时函数的this就指向了obj
    delete obj._fn; // 调用完毕后，在obj对象中删除fn属性
    return result; // 返回函数调用结果
}

Function.prototype.call = myCall;

let obj = {
    name: 'obj'
};
function logMyName() {
    console.log(this.name);
}

logMyName.call(obj); // obj
```

## apply

### 简介

与call类似，只是接受参数的方式有所不同

```javascript
func.apply(thisArg, [argsArray]);
```

### 实现

```javascript
function myApply(obj, args) {
    obj = obj || window; // call对象为null情况下指向window
    obj._fn = this; // 将函数设置为obj的属性
    let result = obj._fn(...args); // 调用函数，此时函数的this就指向了obj
    delete obj._fn; // 调用完毕后，在obj对象中删除fn属性
    return result; // 返回函数调用结果
}

Function.prototype.apply = myApply;
```

## bind

### 简介

bind方法创建一个新的函数，当这个新函数被调用时this为其提供的值，其参数列表前几项值为创建时指定的参数序列。

### 实现

```javascript
function myBind(obj, ...args) {
    let self = this; // 记录函数
    let fNOP = function(){}; // 空对象用于原型继承

    let fBound = function (...args2) {
        return self.apply(this instanceof fNOP ? this : obj, [...args, ...args2]); // 如果this原型链上有fNOP则说明被new调用，则借用构造函数
    };

    fNOP.prototype = this.prototype; 
    fBound.prototype = new fNOP(); // 利用空函数让fBound.prototype能访问到this.prototype
    return fBound;
}

Function.prototype.bind = myBind;
```

## new

### 简介

new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象类型之一

### 实现

```javascript
function myNew(fn, ...args) {
    let F = function () {}; // 空函数
    F.prototype = fn.prototype; // 原型链接
    let obj = new F(); // 继承

    let temp = fn.apply(obj, args);
    return typeof temp === 'object' ? temp : obj; // 如果返回值是对象则返回对象
}

function Person(name) {
    this.name = name;
    this.sex = 'man';
}

console.log(myNew(Person, 'hong')) // Person { name: 'hong', sex: 'man' }
```

## 参考

> [https://github.com/mqyqingfeng/Blog](https://github.com/mqyqingfeng/Blog)
