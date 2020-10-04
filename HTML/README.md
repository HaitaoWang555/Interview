## 你是如何理解 HTML 语义化的
  - 便于机器的识别 便于搜索引擎搜索，有助于爬虫抓取有效信息
  - 代码结构更合理 页面更整洁便于开发者的开发与维护
  - 支持更多类型的机器识别


## meta viewport 是做什么用的，怎么写
  - 为viewport（视口）的初始大小提供指示
  ```HTML
  <!-- width 定义 viewport 的宽度，如果值为正整数，则单位为像素 -->
  <!-- initial-scale 定义设备宽度与 viewport 大小之间的缩放比例 -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  ```

## 你用过哪些 HTML 5 标签？

  ```HTML
  <header> <footer> <main> <nav> <section> <datalist> <dialog>
  ```

## link 外部资源链接元素

  ```HTML
  <!-- 在满足媒体条件的情况下才被加载进来 -->
  <link href="print.css" rel="stylesheet" media="print">
  <link href="mobile.css" rel="stylesheet" media="screen and (max-width: 600px)">

  <!-- preload 预加载 as 特定的内容类。crossorigin属性表示该资源是否应该使用一个CORS请求来获取 -->
  <link rel="preload" href="myFont.woff2" as="font" type="font/woff2" crossorigin="anonymous">

  <!-- 样式表加载事件 -->
  <link rel="stylesheet" href="mystylesheet.css" onload="sheetLoaded()" onerror="sheetError()">

  ```

## script async defer
  - 对于普通脚本，如果存在 async 属性，那么普通脚本会被并行请求，并尽快解析和执行。该属性能够消除解析阻塞的 Javascript

  - defer被设定用来通知浏览器该脚本将在文档完成解析后，触发 DOMContentLoaded 事件前执行

