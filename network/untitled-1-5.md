# GET POST 区别

1. GET使用URL或Cookie传参，而POST将数据放在BODY中”，这个是因为HTTP协议用法的约定。并非它们的本身区别。
2. GET方式提交的数据有长度限制，则POST的数据则可以非常大”，这个是因为它们使用的操作系统和浏览器设置的不同引起的区别。也不是GET和POST本身的区别。
3. POST比GET安全，因为数据在地址栏上不可见”，这个说法没毛病，但依然不是GET和POST本身的区别。
4. GET和POST最大的区别主要是GET请求是幂等性的，POST请求不是。这个是它们本质区别，上面的只是在使用上的区别。（什么是幂等性？幂等性是指一次和多次请求某一个资源应该具有同样的副作用。简单来说意味着对同一URL的多个请求应该返回同样的结果。）
