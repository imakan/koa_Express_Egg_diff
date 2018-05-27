# koa 与 express 与 connect 与 egg 区别

##  express

>  Express是一个简洁灵活的web开发框架，使用简单而功能强大

> koa 是express框架原班人马基于es6新特性重新开发的敏捷开发框架

> egg 底层基于 Koa 1.x，异步解决方案基于 co 封装的 generator function

  **为什么koa不定义为express4.0**

  Koa与人们所知的Express有很大的不同，设计基本上不同，所以从Express3.0到4.0迁移，需要重写整个应用

服务端开发框架，主要是对HTTP Request 以及 HTTP Response两个对象的封装和处理，应用的生命周期维护以及视图的处理等

1、express 主要基于Connect 中间件框架，功能丰富，随取随用，``框架自身封装了大量便利的功能``，路由，视图处理.

2、koa主要基于co中间件框架，框架自身没有继承太多功能，所以要require去解决，使用promises和async functions来清除callback hell的应用程序并简化错误处理。它暴露自己ctx.request和ctx.response对象，而不是节点req和res对象，only about 2K lines of code。（虽然express 也有co-express，取决于你喜欢怎么写）

3、connect与koa中间件模式区别的核心就在于next的实现

| Feature           | Koa | Express | Connect |
|------------------:|-----|---------|---------|
| Middleware Kernel | ✓   | ✓       | ✓       |
| Routing           |     | ✓       |         |
| Templating        |     | ✓       |         |
| Sending Files     |     | ✓       |         |
| JSONP             |     | ✓       |         |


## Koa 与 Express 以及 Connect 的区别

![koa](https://user-gold-cdn.xitu.io/2017/8/7/eaa60fcf179c834c9f010151a5b360cf?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

1、基于promise的控制流程,洋葱圈比Express强大

2、Koa是准系统（application.js, context.js, request.js, response.js）

* 2.1 koa 不包含任何中间件

* 2.2 不提供路由

* 2.3 更加模块化

3、Koa抽象节点的请求/相应 （更加好的用户体验）


## koa 与 express 性能测试

* Windows 10 PC Ubuntu子系统i7-3612QM 8GB内存。

* Azure d系列Ubuntu Linux VM，有4个vCPUs和16GB内存。

> 测试使用 Apache Bench 来度量请求性能。每个框架基准测试重复5次，最后的结果是5次测试的平均值。

> Software Versions Tested NodeJS v9.11.1 ExpressJS v4.16.3 Koa2 v2.5.0

```
Windows 10 Ubuntu Subsystem: | Framework | req/s | |–|–| | Node| 1253.358 | | Express| 1352.154 | | Koa2| 1284.026 |
```

```
Azure D-Series Ubuntu VM | Framework | req/s | |–|–| | Node| 7894.918 | | Express| 4786.654 | | Koa2| 5401.43 |
```

![express vs Koa2](https://raygun.com/blog/images/KoaExpress.jpg)

### 结论

在性能方面，Koa以一个微弱的优势险胜Express，如果有显著的性能要求，应考虑Koa的优势


##  总结

* 如果是一个纯净的应用，可读性比较好，比较清晰的逻辑 适合用koa
* 如果现有项目已经是Express的应用程序,应该坚持Express，Koa与Express并不能很容易的合作，Koa的Context对象与基本的Node req和 res对象不兼容
* 性能上Koa 比 Express 有轻微的优势
* 如果你喜欢diy，很潮，可以考虑koa，它有足够的扩展和中间件，而且自己写很简单
* 如果你想简单点，找一个框架啥都有，那么先express

## koa 与 egg

Egg 1.x 发布时，Node.js 的 LTS 版本尚不支持 async function，所以 Egg 1.x 仍然基于 Koa 1.x 开发，但是在此基础上，Egg 全面增加了 async function 的支持，再加上 Egg 对 Koa 2.x 的中间件也完全兼容，应用层代码可以完全基于 async function 来开发。

* 底层基于 Koa 1.x，异步解决方案基于 co 封装的 generator function

* 官方插件以及 Egg 核心使用 generator function 编写，保持对 Node.js LTS 版本的支持，在必要处通过 co 包装以兼容在 async function 中的使用。

* 应用开发者可以选择 async function（Node.js 8.x+） 或者 generator function（Node.js 6.x+）进行编写。

Node.js 8 正式进入 LTS 后，async function 可以在 Node.js 中使用并且没有任何性能问题了，Egg 2.x 基于 Koa 2.x，框架底层以及所有内置插件都使用 async function 编写，并保持了对 Egg 1.x 以及 generator function 的完全兼容，应用层只需要升级到 Node.js 8 即可从 Egg 1.x 迁移到 Egg 2.

* 底层基于 Koa 2.x，异步解决方案基于 async function。

* 官方插件以及 Egg 核心使用 async function 编写。

* 建议业务层迁移到 async function 方案。

* 只支持 Node.js 8 及以上的版本。



## 总结

Egg 是在 Koa 上作了强约束，规定代码编写、目录结构等。


---
题外话：express 的作者和维护者（TJ、 Jonathan）弃坑从 express 转向开发 koa 


## 借鉴资料

https://eggjs.org/zh-cn/intro/egg-and-koa.html
https://github.com/eggjs/egg/issues/159
https://github.com/eggjs/egg/issues/1105
https://alili.tech/2017/12/13/Nodejs/%E5%BC%80%E5%90%AFExpress%EF%BC%8CEgg.js%EF%BC%8CKoa.js%20%E7%9A%84Gzip%E6%A8%A1%E5%BC%8F/
https://cnodejs.org/topic/55815f28395a0c1812f18257
https://yq.aliyun.com/articles/3062
https://blog.csdn.net/k616358281/article/details/71602055
https://www.v2ex.com/t/381730
http://www.jb51.net/article/133633.htm
https://raygun.com/blog/koa-vs-express-2018/
https://github.com/koajs/koa/blob/master/docs/koa-vs-express.md