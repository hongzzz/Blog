# HTTP 缓存机制

> 重用已获取的资源能够有效的提升网站与应用的性能。Web 缓存能够减少延迟与网络阻塞，进而减少显示某个资源所用的时间。借助 HTTP 缓存，Web 站点变得更具有响应性。

## 强制缓存

强制缓存通过 **Expires** 和 **Cache-Control** 来控制，它们都是用来标志资源过期时间的首部。

优先级 **Cache-Control** > **Expires**

缓存可用情况下在chrome表现为`200 OK(from cache)`

### Expires

http1.0时期的产物，Expires的值对应一个GMT，不超过这个时间则不发送新请求。如

```
Expires: Wed, 09 Jan 2019 05:28:54 GMT
```

### Cache-Control

http1.1中定义，常见值有**private**，**public**，**no-cache**，**max-age**，**no-store**，默认为 **private**

```
Cache-Control: max-age=3600
```

max-age 单位为秒，如上则表示一个小时内请求此资源不用重新发送请求

max-age 和 Expires 同时存在的情况下，忽略 Expires

## 协商缓存

如果上述过程都不成功，那么客户端会向服务器发出一个请求，服务器对比后返回对应 **304** 或者 **200**

优先级 **ETag** > **Last-Modified**

### Last-Modified

**Last-Modified** 响应头对应 **If-Modified-Since** 请求头

客户端第一次请求资源时，服务器响应首部携带 **Last-Modified** 资源修改的最后时间

客户端再次访问资源时，请求首部携带 **If-Modified-Since**，服务器收到后与该资源最后修改时间比较，如果修改时间大于 **If-Modified-Since** 携带的时间，则响应 **200** 并携带资源内容，否则返回 **304**，浏览器会使用之前的cache

### ETag

**ETag** 响应头对应 **If-None-Match** 请求头

客户端第一次请求资源时，服务器响应首部携带生成的 **ETag**

客户端再次访问资源时，请求首部携带 **If-None-Match**，服务器比较现在资源标记是否改变，改变的话则返回 **200**，否则返回 **304** 并使用cache，与 **Last-Modified** 过程基本一致

## 用户刷新行为

### 直接访问网址

如果通过 **Cache-Control** 发现资源被缓存并且没有过期，则直接使用cache中的

### F5刷新

刷新后，即使资源未过期，也会发送一个请求到服务器，通过 **ETag** 或者 **Last-Modified** 验证资源是否改动

### Ctrl+F5强制刷新

同样发请求到服务器，但是请求头部不携带 **If-Modified-Since** 或者 **If-None-Match**，让服务器不能比较资源是否改动，只能返回完整的资源
