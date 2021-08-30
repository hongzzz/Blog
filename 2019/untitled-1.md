# 防抖 & 节流

## Debounce - 防抖

* 在某段连续时间内, 在事件触发后只执行一次
* 主要应用场景：文本输入keydown 事件, keyup 事件

  ```javascript
  function debounce(fn, delay) {
  let timer;
  return function () {
    let context = this;
    let args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function () {
      fn.apply(context, args);
    }, delay);
  }
  }
  ```

## Throttle - 节流

* 设置固定的函数执行速率, 从而降低频繁事件回调的执行次数
* 主要应用场景:鼠标移动, mousemove 事件, DOM 元素动态定位, window对象的resize和scroll 事件

  ```javascript
  function throttle(fn, threshhold = 250) {
  let last;
  let timer;
  return function () {
    let context = this;
    let args = arguments;
    let now = +new Date();
    if (last && now < last + threshhold) { // 超出时间了则直接执行一次，否则clearTimeout
      clearTimeout(timer);
      timer = setTimeout(function () {
        last = now;
        fn.apply(context, args)
      }, threshhold)
    } else {
      last = now;
      fn.apply(context, args);
    }
  }
  }
  ```

