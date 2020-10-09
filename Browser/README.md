## 事件机制

## 事件委托

## 什么是 JSONP，什么是 CORS，什么是跨域？

## 事件循环_执行栈_宏任务_微任务

## cookie，localStorage，sessionStorage，indexDB

  - cookie是存储在浏览器上的一小段数据，用来记录某些当页面关闭或者刷新后仍然需要记录的信息；可以使用 js 在浏览器直接设置也可以在服务端通使用 HTTP 协议规定的 set-cookie 来让浏览器种下cookie；每次网络请求 Request headers 中都会带上cookie，最大容量为4k

  - session存在服务器内存中，也可保存在数据库中；创建session后，会把关联的session_id 通过setCookie 添加到http响应头部中，浏览器在加载页面时发现响应头部有 set-cookie 字段，就把这个 cookie 种到浏览器指定域名下，发送的请求会带上这条cookie， 服务端在接收到后根据这个来识别用户。

  - localStorage是本地存储web storage特性的API之一，用于将大量数据（最大5M）保存在浏览器中，保存后数据永远存在不会失效过期，除非用 js手动清除；不参与网络传输；一般用于性能优化，可以保存图片、js、css、html 模板、大量数据

## 渲染机制

## 回流重绘

## 性能
