# JS 事件循环

为了避免多线程操作之间的带来的同步问题，JavaScript从设计以来就是一门单线程的语言

虽说HTML5提出了Web Worker标准使JavaScript能创建多个线程，但是子线程完全受主线程控制，并且没有执行I/O操作的权限，只能帮主线程完成一些计算工作，严格来说没有改变JavaScript单线程的本质

## 任务队列 Task Queue

于是为了不让执行时间长的任务阻塞住线程（例如AJAX操作），JavaScript把任务分为两种，一种是**同步任务**，一种是**异步任务**。同步任务在主线程上执行完毕才能执行下一个任务，异步任务先进入**任务队列**，等某个异步任务到执行的时间了并且主线程空闲，该任务才会进入主线程被执行。

## 事件循环 Event Loop

JavaScript遇到一个异步任务时，会暂时将这个任务加入任务队列，先执行其他同步任务。当同步任务都执行完毕后，主线程在空闲时会找任务队列中是否有任务可以执行，如果有的话取出任务并在主线程执行其中的同步代码，把其中的异步任务放入事件队列，执行完后再从任务队列找新的任务...

这个循环就是Event Loop（事件循环）

![event loop](http://www.ruanyifeng.com/blogimg/asset/2014/bg2014100802.png)

## Microtasks & Macrotasks

任务队列不止有一个，异步任务又细分为Microtasks和Macrotasks，即微任务与宏任务，他们分别在不同的队列中。

* **macrotasks**: `setTimeout`, `setInterval`, `setImmediate`, `requestAnimationFrame`,I/O, UI rendering
* **microtasks**: `process.nextTick`, `Promise`, `Object.observe`(废弃), `MutationObserver`

每个事件循环中，从Marcotasks队列中取一个任务执行，再执行完Microtasks队列中的任务，接着进入下一个事件循环。

## 例子

```javascript
console.log('load script');
setTimeout(function () {
    Promise.resolve().then(()=>{
        console.log('promise')
    });
    console.log('setTimeout');
}, 0);
new Promise((resolve) => {
    console.log('resolve');
    resolve();
}).then(() => {
    console.log('then1');
}).then(()=>{
    console.log('then2');
});
console.log('script end');
```

### 循环1

1. 输出'load script'
2. setTimeout回调加入macrotasks队列
3. 执行Promise里内容，输出'resolve'
4. Promise.then 1,2 加入microtasks队列
5. 输出'script end'
6. 清空当前microtasks，输出'then1' 'then2'

### 循环2

1. 取出setTimeout回调并执行
2. Promise.then加入microtasks队列
3. 输出'setTimeout'
4. 清空microtasks，输出'promise'

## 参考

[http://www.ruanyifeng.com/blog/2014/10/event-loop.html](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)

[https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/) （有效果图，有帮助理解）

[https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)

[https://github.com/ccforward/cc/issues/47](https://github.com/ccforward/cc/issues/47)
