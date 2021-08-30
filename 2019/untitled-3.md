# CSS BFC

**块格式化上下文（Block Formatting Context，BFC）** 是Web页面的可视化CSS渲染的一部分，是布局过程中生成块级盒子的区域，也是浮动元素与其他元素的交互限定区域。

## 触发条件

1. 根元素，即HTML元素
2. float的值不为none
3. overflow的值不为visible
4. display的值为inline-block、table-cell、table-caption
5. position的值为absolute或fixed

## 特性

1. 属于同一个BFC的两个相邻Box的margin会发生重叠
2. 每个元素的margin box的左边， 与包含块border box的左边相接触
3. BFC的区域不会与float box重叠
4. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
5. 计算BFC的高度时，浮动元素也参与计算（可用于清除浮动）

