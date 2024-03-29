# 前端性能优化

## 构建优化

1. **tree-shaking** 删除未使用的代码
2. **code-splitting** 代码分块，便于代码的按需加载，分离第三方模块便于缓存

## 渲染优化

1. CSS放于页面顶部（一次性生成CSSOM TREE，避免多次渲染）
2. JS放于页面底部（防止JS运行阻塞页面渲染）
3. 服务端渲染（在服务端渲染出首页，避免客户端首页渲染时间过长）
4. 首页渲染（让用户先看到加载动画）
5. 图片懒加载（避免一次性请求太多图片资源）
6. 使用 **requestAnimationFrame** 代替 **setTimeout** 完成动画（避免动画掉帧）

## 网络请求优化

1. 使用CDN
2. 使用HTTP/2
3. 避免重定向
4. 比较小的图片可以使用base64形式内嵌到HTML中（体积会比原大33%左右）
5. CSS雪碧图（将多张图片合成一张）
6. 强缓存，协商缓存（减少不必要请求）

## 资源压缩

1. JS压缩与混淆（**uglifyjs**）
2. CSS压缩（**postcss** => **cssnano**）
3. HTML压缩
4. 图片压缩
5. 开启 **GZIP**

****

{% @mailchimp/mailchimpSubscribe %}
