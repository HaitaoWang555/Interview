## 有哪些常见 loader 和 plugin，你用过哪些？

    - babel-loader：把 ES6 转换成 ES5
    - file-loader:把文件输出到文件夹，文件中通过url 引入代码
    - url-loader：跟file-loader 相似，但是小文件可以处理成base64 加到文件代码中去
    - source-map-loader：加载额外的 Source Map 文件，以方便断点调试
    - css-loader:加载css，压缩 格式化 文件导入css 
    - style-loader：把css 加载到js 中去
    - image-loader：加载并且压缩图片文件
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

  - 多入口情况下，使用CommonsChunkPlugin来提取公共代码
  - 通过externals配置来提取常用库
  - Happypack 使用多线程打包
  - 利用DllPlugin和DllReferencePlugin预编译资源模块 通过DllPlugin来对那些我们引用但是绝对不会修改的npm包来进行预编译，再通过DllReferencePlugin将预编译的模块加载进来。
  - 使用webpack-uglify-parallel来提升uglifyPlugin的压缩速度。 原理上webpack-uglify-parallel采用了多核并行压缩来提升压缩速度
  - 缓存构建:webpack构建中,可以通过设置cacheDirectory来达到缓存的目的。
  - 通过配置resolve.modules来告诉webpack解析模块时应该搜索的目


## 转义出的文件过大怎么办

  - ExtractTextPlugin：提取样式到css文件
  - CommonsChunkPlugin：提取通用模块文件
  - 压缩 JS、CSS、图片
  - 按需加载
  - 使用splitChunks来进行拆包,抽离第三方依赖库
