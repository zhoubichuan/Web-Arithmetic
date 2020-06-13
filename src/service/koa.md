---
lang: zh-CN
sidebarDepth: 2
meta:
  - name: description
    content: 个人总结的vuepress学习技术文档-主题
  - name: keywords
    content: vuepress,最新技术文档,vuepress主题
---

# koa

## 1. koa 和 express 的区别

* 异步流程的控制：express 采用 callback 来处理异步，koa2 采用的是 async/await
* 错误处理：express 采用 callback 捕获异常，对深层次的异常捕获不了，koa 采用 try/catch
## 2. koa 中间件执行机制

* 添加中间件的方式是使用 koa 实列的 use 方法，并传入一个 generator 函数，这个 generator 函数接受一个 next 参数
* use 的原理：function Application(){
  this.middleware =[]
  }
* 每次执行 use 方法，就把外面传进来的 generator 函数 push 到 middleware 数组中
* koa 中是预先通过 use 方法，将请求可能会经过的中间件装在一个数组中
* callback 函数就是请求到来的事件执行的回调。把装着中间件 middleware 的数组作为参数传递为 compose 这个方法
* componse 把毫无关系的一个一个中间件给收尾串起来了，就好比我们平常的烤面筋
* 作为参数传递给前一个中间件，当最后一个中间件的参数 next 是空的 generator 函数生成对象
