## 生命周期
  `beforeCreate`
  `created`
  `beforeMount`
  `mounted`
  `beforeUpdate` 数据更新时调用，发生在虚拟 DOM 打补丁之前
  `updated` 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子
  `activated` 被 keep-alive 缓存的组件激活时调用。
  `deactivated` 被 keep-alive 缓存的组件停用时调用。
  `beforeDestroy`
  `destroyed`

## NextTick

  `nextTick` 可以让我们在下次 DOM 更新循环结束之后执行延迟回调，用于获得更新后的 DOM。
  `Promise.then`、`MutationObserver` 和 `setImmediate`，如果执行环境不支持，则会采用 setTimeout(fn, 0) 代替

## watch 和 computed 和 methods 区别是什么？

  - computed 和 methods 相比，最大区别是 computed 有缓存：如果 computed 属性依赖的属性没有变化，那么 computed 属性就不会重新计算。methods 则是看到一次计算一次。
  - watch 和 computed 相比，computed 是计算出一个属性（废话），而 watch 则可能是做别的事情（如上报数据）

## Vue 如何实现组件间通信？

  - props
  - .sync 
  - $attrs 和 $listeners
  - $parent 和 $children
  - eventBus
  ```js
  var eventBus = new Vue()
  eventBus.$emit() 
  eventBus.$on()
  ```
  - provide/inject
  - Vuex
  - ref

## Vue 数据响应式怎么做到的？

  - Object.defineProperty
    弊端：
      - 需要对原始数据克隆
      - 需要分别给对象中每一个属性设置监听
      - 不能监听的可以用$set强制监听，数组的方法重写了
  - Proxy

## Vuex

  - State 定义了应用状态的数据结构，可设置默认的初始状态
  - Getter this.$store.getters mapGetters 获取
  - Mutation 更改 Vuex 的 store 中的状态的唯一方法是提交 mutation
  - Action Action 类似于 mutation，不同在于 Action 提交的是 mutation，而不是直接变更状态 Action 可以包含任意异步操作
  - Module 分模块

## VueRouter

  - vue-router在单页面应用中,主要用于组件之间的切换。其本质就是:建立并管理url和对应组件之间的映射关系.
  - `<router-link></router-link>` `<router-view />`
  ```js
    // 这个方法会向 history 栈添加一个新的记录
    router.push()
    // params  path
    router.push({ name: 'user', params: { userId }}) // -> /user/123
    router.push({ path: `/user/${userId}` })
    // 替换掉当前的 history 记录
    router.replace()
    // 在 history 记录中向前或者后退多少步
    router.go(n)
  ```

## 路由守卫是什么？
  ```js
  // 全局前置守卫
  router.beforeEach((to, from, next) => {
    // ...
  })
  // 全局解析守卫 在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后，解析守卫就被调用
  router.beforeResolve((to, from, next) => {
    // ...
  })
  
  // 全局后置钩子
  router.afterEach((to, from) => {
    // ...
  })

  // 组件内的守卫
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
  ```

## v-if和v-for哪个优先级更高？
  - v-for优先于v-if被解析
  - 为了过滤列表中的项目 定义一个计算属性，让其返回过滤后的列表即可
  - 为了避免渲染本应该被隐藏的列表，此时把 v-if 移动至容器元素上

## key的作用
  - key的作用主要是为了更高效的更新虚拟DOM。
  - 判断两个节点是否是相同节点 key是一个必要条件

## 双向绑定以及它的实现原理

  - `v-model` 指令在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定, 它会根据控件类型自动选取正确的方法来更新元素
  - v-model是语法糖，默认情况下相当于:value和@input。
