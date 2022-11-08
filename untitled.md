# JS 模块化

## CommonJS模块

这个规范主要用于Node.js上

使用`require`加载模块, 加载模块后会执行整个脚本并在内存生成一个`Module`对象。以后再调用这个模块时,就会在缓存中找到这个对象,并在对象上的`exports`属性上取值,不会重复执行该模块

```javascript
Module {
  id: ..., // 模块名
  exports: { ... }, // 模块输出
  parent: ..., // 父模块
  filename: ..., // 文件路径
  loaded: false, // 模块是否运行完毕
  children: [ ... ], // 子模块
  paths:[ ... ]  // 模块可能的位置
}
```

`module.exports`是一个对象,在脚本执行完毕后才会生成

## ES6模块

使用`import`加载模块,第一时间不会执行模块,只是产生一个引用,等到需要时再到模块中取值

使用`export`规定模块对外接口,与`CommonJS`不同,是一种静态定义,在代码解析阶段就会生成

## ES6模块与CommonJS差异

1. CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
2. CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。

## AMD & CMD

​ **AMD 推崇依赖前置、提前执行**，**CMD推崇依赖就近、延迟执行**。AMD 是 **RequireJS** 在推广过程中对模块定义的规范化产出。CMD 是 **SeaJS** 在推广过程中对模块定义的规范化产出。

```javascript
/** AMD写法 **/
define(["a", "b", "c", "d", "e", "f"], function(a, b, c, d, e, f) { 
    // 等于在最前面声明并初始化了要用到的所有模块
   a.doSomething();
   if (false) {
       // 即便没用到某个模块 b，但 b 还是提前执行了
       b.doSomething()
   } 
});

/** CMD写法 **/
define(function(require, exports, module) {
   var a = require('./a'); //在需要时申明
   a.doSomething();
   if (false) {
       var b = require('./b');
       b.doSomething();
   }
});
```
