# 深拷贝、浅拷贝

js中基本类型（number,string,null,undefined,boolean,symbol）存放在栈中，基本类型值不可变

引用类型（object）存在在堆中，变量实际上保存的是一个指针，指向堆内存中的地址，引用类型值可变

## 浅拷贝

遍历对象第一层属性，并只拷贝对象的第一层属性，往下层的对象还是指向堆中的同一个对象

### 实现

```javascript
function shallowCopy(obj) {
    let newObj = obj instanceof Array ? [] : {}; // 区分数组与对象
    for (let key in obj) { // 遍历obj的属性
        if (obj.hasOwnProperty(key)) { // 排除原型上的属性
            newObj[key] =  obj[key]; // 只复制第一层，往下层的对象还是指向同一个对象
        }
    }
    return newObj;
}

let parent = {
    name: 'parent',
    child: {
        name: 'child'
    }
}；
let parent2 = shallowCopy(parent);
parent2.child.name = 'changed child';

console.log(parent.child.name); // 'changed child' 
console.log(parent2.child.name); // 'changed child'
```

## 深拷贝

遍历对象属性，如果下层还是一个对象的话就递归调用函数，从而把所有属性都拷贝一遍

### 实现

```javascript
function deepCopy(obj) {
    if (typeof obj !== 'object') return obj; // 如果是基础类型则直接返回
    let newObj = obj instanceof Array ? [] : {}; // 区分数组与对象
    for (let key in obj) { // 遍历obj的属性
        if (obj.hasOwnProperty(key)) { // 排除原型上的属性
            newObj[key] = typeof obj[key] === 'object' ? deepCopy(obj[key]) : obj[key]; // 如果还是对象的话则递归调用
        }
    }
    return newObj;
}

let parent = {
    name: 'parent',
    child: {
        name: 'child'
    }
}；
let parent2 = deepCopy(parent);
parent2.child.name = 'changed child';

console.log(parent.child.name); // 'child' 
console.log(parent2.child.name); // 'changed child'
```
