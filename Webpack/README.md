## 有哪些常见 loader 和 plugin，你用过哪些？

    - babel-loader：编译es6代码的
    - file-loader:把文件输出到文件夹，文件中通过url 引入代码
    - url-loader：跟file-loader 相似，但是小文件可以处理成base64 加到文件代码中去
    - css-loader:加载css，压缩 格式化 文件导入css 
    - style-loader：把css 加载到js 中去
    - image-loader：处理图片
    - define-plugin：定义环境，可以通过设置不同环境打对应的包
    - common-chunks-plugin：提取公共代码
    - uglifyjs-webpack-plugin: 压缩js 代码

## webpack loader 和 plugin 的区别

  - loader 加载器，webpack把一切文件视为模块，原本webpack 只能解析js文件，有了loader之后可以加载其他文件了，loader的作用就是能支持加载其他文件， 通过module.rules 中配置不同的loader rules 是一个数组，里面每项是个对象，检查不同类型的文件用不同loader 处理。
  - plugin 插件，让webpack的功能更强大，可以在webpack的运行不同时期监听不同事件，做不同的事。通过在plugins 里面配置

## webpack的构建流程
1. 初始化参数：从配置文件和shell语句中读取合并参数，等到最终参数
2. 开始编译：用上一步得到的参数生成compiler 对象，加载所有的插件，并执行对象的run 方法开始编译
3. 确定入口：根据entry 找到所有的入口
4. 编译模块：从入口文件出发，调用所有配置的loader对模块
5. 完成模块编译
6. 输出资源

## 如何按需加载代码？

  - 组件库的按需加载 `babel-plugin-component(elementui)`
  - ES modules 的 tree shaking

## 如何提高构建速度？


## 转义出的文件过大怎么办

