## 浏览器事件
  - 事件传播的 3 个阶段
    1. 捕获阶段（Capturing phase）—— 事件（从 Window）向下走近元素
    2. 目标阶段（Target phase）—— 事件到达目标元素
    3. 冒泡阶段（Bubbling phase）—— 事件从元素上开始冒泡

  - 注册事件
  ```js
  /**
  * type 表示监听事件类型的字符串。
  * listener 处理程序。
  * options.once 如果为 true，那么会在被触发后自动删除监听器
  * options.capture options 也可以是 false/true，它与 {capture: false/true} 相同 如果为 false（默认值），
  则在冒泡阶段设置处理程序 如果为 true，则在捕获阶段设置处理程序
  * options.passive 如果为 true，那么处理程序将不会调用 preventDefault()
  */
  target.addEventListener(type, listener, options);
  ```
  - 停止冒泡
  用于停止冒泡的方法是 `event.stopPropagation()`
  `event.stopImmediatePropagation()`可以用于停止冒泡，并阻止当前元素上的处理程序运行

  - 事件代理

    如果一个节点中的子节点是动态生成的，那么子节点需要注册事件的话应该注册在父节点上

## 什么是 JSONP，什么是 CORS，什么是跨域？
 
  - 如果协议、域名或者端口有一个不同就是跨域
  - JSONP 的原理很简单，就是利用 `<script>` 标签没有跨域限制的漏洞。通过 `<script>` 标签指向一个需要访问的地址并提供一个回调函数来接收数据。
  JSONP 使用简单且兼容性不错，但是只限于 `get` 请求。
    ```js
    <script src="http://domain/api?param1=a&param2=b&callback=jsonp"></script>
    <script>
        function jsonp(data) {
          console.log(data)
      }
    </script>    
    ```
  - 服务端设置 `Access-Control-Allow-Origin` 就可以开启 CORS。 该属性表示哪些域名可以访问资源，如果设置通配符则表示所有网站都可以访问资源

## 运行时(Runtime) 栈(Stack) 堆(Heap) 队列(Queue)
  - 运行时
  ![](https://mdn.mozillademos.org/files/17124/The_Javascript_Runtime_Environment_Example.svg)
  - 栈 函数调用形成了一个由若干帧组成的栈。
  - 堆 对象被分配在堆中，堆是一个用来表示一大块（通常是非结构化的）内存区域的计算机术语。
  - 队列 一个 JavaScript 运行时包含了一个待处理消息的消息队列


## 事件循环(event loop) 宏任务(macrotasks) 微任务(microtask)
  - 事件循环是一个在 JavaScript 引擎等待任务，执行任务和进入休眠状态等待更多任务这几个状态之间转换的无限循环
  - 一个任务到来时，引擎可能正处于繁忙状态，那么这个任务就会被排入队列。多个任务组成了一个队列，即所谓的“宏任务队列
  - 引擎执行任务时永远不会进行渲染（render）。仅在任务完成后才会绘制对 DOM 的更改。
  - 如果一项任务执行花费的时间过长，浏览器将无法执行其他任务，无法处理用户事件，因此，在一定时间后浏览器会在整个页面抛出一个如“页面未响应”之类的警报，建议你终止这个任务。这种情况常发生在有大量复杂的计算或导致死循环的程序错误时
  - 异步任务需要适当的管理。为此，ECMA 标准规定了一个内部队列 PromiseJobs，通常被称为“微任务队列
  - 事件循环图 每个宏任务之后，引擎会立即执行微任务队列中的所有任务，然后再执行其他的宏任务，或渲染，或进行其他任何操作。
  ![](https://zh.javascript.info/article/event-loop/eventLoop-full.svg)
  - 使用零延迟的 setTimeout(f) 可被用于将繁重的计算任务拆分成多个部分，以使浏览器能够对用户事件作出反应，并在任务的各部分之间显示任务进度。

## cookie，localStorage，sessionStorage，indexDB

  - cookie是存储在浏览器上的一小段数据，用来记录某些当页面关闭或者刷新后仍然需要记录的信息；可以使用 js 在浏览器直接设置也可以在服务端通使用 HTTP 协议规定的 set-cookie 来让浏览器种下cookie；每次网络请求 Request headers 中都会带上cookie，最大容量为4k

  - session存在服务器内存中，也可保存在数据库中；创建session后，会把关联的session_id 通过setCookie 添加到http响应头部中，浏览器在加载页面时发现响应头部有 set-cookie 字段，就把这个 cookie 种到浏览器指定域名下，发送的请求会带上这条cookie， 服务端在接收到后根据这个来识别用户。

  - localStorage是本地存储web storage特性的API之一，用于将大量数据（最大5M）保存在浏览器中，保存后数据永远存在不会失效过期，除非用 js手动清除；不参与网络传输；一般用于性能优化，可以保存图片、js、css、html 模板、大量数据

## 渲染机制
  1. 处理 HTML 并构建 DOM 树。
  2. 处理 CSS 构建 CSSOM 树。
  3. 将 DOM 与 CSSOM 合并成一个渲染树。
  4. 根据渲染树来布局，计算每个节点的位置。
  5. 调用 GPU 绘制，合成图层，显示在屏幕上。

## 重绘（Repaint）和回流（Reflow）
  - 重绘是当节点需要更改外观而不会影响布局的，比如改变 `color` 就叫称为重绘
  - 回流是布局或者几何属性需要改变

## 性能工具
  - 性能工具让你深入了解你的网站的一般响应性，JavaScript和布局性能
  - Waterfall（瀑布流）展示浏览器所做的不同工作，如运算布局，JavaScript，重绘，和垃圾回收
  - Call Tree（调用树）展示那些最耗时间的JavaScript函数
  