# 回流 & 重绘

## Repaint 重绘

Repaint 只需更新某个元素样式

### 触发条件：

* 页面中的元素更新样式风格相关的属性时就会触发重绘，如background，color，cursor，visibility，etc

## Reflow 回流

Reflow 需要重新计算整个文档元素位置

### 触发条件：

* 盒模型相关的属性: width, height, margin, display, border, etc
* 定位属性及浮动相关的属性: top, position, float，etc
* 改变节点内部文字结构也会触发回流: text-align, overflow, font-size, line-height, vertical-align, etc
* 调整窗口大小
* 样式表变动
* 元素内容变化，尤其是输入控件
* dom操作
* css伪类激活
* 计算元素的offsetWidth、offsetHeight、clientWidth、clientHeight、width、height、scrollTop、scrollHeight

## 优化

* 替代触发回流重绘的属性，比如用translate代替top，用opacity替代visibility
* 减少reflow操作，直接更改classname或者cssText
* 频繁reflow的元素可以使用DocumentFragment缓存，或者先display:none，只触发两次回流与重绘
* 创建新图层，避免外层回流重绘

**由页面的渲染过程可知，reflow必将会引起repaint，而repaint不一定会引起reflow**

参考 [reflow和repaint引发的性能问题 - 掘金](https://juejin.im/post/5a9372895188257a6b06132e)

另外图层相关知识可看 [无线性能优化：Composite](http://taobaofed.org/blog/2016/04/25/performance-composite/)
