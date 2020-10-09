## 内置类型

  - `null`,`undefined`,`boolean`,`number`,`string`,`symbol`, `BigInt`
  - `object`

## ES6 语法知道哪些,分别怎么用

  - `let`、`const`
  - 箭头函数
  - 变量的解构赋值
  - 模板字符串
  - 数组的扩展 `Array.from()`、`Array.of()`、`Array.find()`、`Array.findIndex()`、`Array.fill()`、`Array.includes()`、`Array.flat()`

## `Promise`、`Promise.all()`、`Promise.race()`、`Promise.allSettled()`分别怎么用
  ```JavaScript
  // 创造了一个Promise实例
  const promise = new Promise(function(resolve, reject) {
    // ... some code

    if (/* 异步操作成功 */){
      resolve(value)
    } else {
      reject(error)
    }
  })

  // Promise 使用
  promise
    .then(result => {···})
    .catch(error => {···})
    .finally(() => {···})

  // Promise.all() 使用
  // 每个实例的状态都变成fulfilled，或者其中有一个变为rejected，才会调用Promise.all方法后面的回调函数
  // 如果任意一个 promise 被 reject，由 Promise.all 返回的 promise 就会立即 reject，如果出现 error，其他 promise 将被忽略，并且带有的就是这个 error
  Promise.all([p1, p2, p3]).then(function (results) {
    // ...
  }).catch(function(error){
    // ...
  })

  // Promise.race() 使用
  // 有一个实例率先改变状态就会调用Promise.race方法后面的回调函数
  Promise.race([p1, p2, p3]).then(function (results) {
    // ...
  }).catch(function(error){
    // ...
  })
  // Promise.allSettled() 使用
  // 等待所有的 promise 都被 settle 会调用Promise.allSettled方法后面的回调函数
  Promise.allSettled([p1, p2, p3]).then(function (results) {
    results.forEach((result, num) => {
      if (result.status == "fulfilled") {
        //
      }
      if (result.status == "rejected") {
        //
      }
    })
  }).catch(function(error){
    // ...
  })

  ```

## 手写函数防抖和函数节流

  防抖和节流的作用都是防止函数多次调用。区别在于，假设一个用户一直触发这个函数，且每次触发函数的间隔小于wait，防抖的情况下只会调用一次，而节流的 情况会每隔一定时间（参数wait）调用函数
  防抖动和节流本质是不一样的。防抖动是将多次执行变为最后一次执行，节流是将多次执行变成每隔一段时间执行。
  ```JavaScript
  // func是用户传入需要防抖的函数
  // wait是等待时间
  const debounce = (func, wait = 50) => {
    // 缓存一个定时器id
    let timer = 0
    // 这里返回的函数是每次用户实际调用的防抖函数
    // 如果已经设定过定时器了就清空上一次的定时器
    // 开始一个新的定时器，延迟执行用户传入的方法
    return args => {
      if (timer) clearTimeout(timer)
      timer = setTimeout(() => {
        func.call(this, args)
      }, wait)
    }
  }
  // 不难看出如果用户调用该函数的间隔小于wait的情况下，上一次的时间还未到就被清除了，并不会执行函数

  const throttle = (func, wait = 50) => {
    let prev, timer
    return function fn() {
      let curr = Date.now()
      let diff = curr - prev
      if (!prev || diff >= wait) {
        func.apply(this, arguments)
        prev = curr
      } else if (diff < wait) {
        clearTimeout(timer)
        timer = setTimeout(fn, wait - diff)
      }
    }
  }

  function ajax (data) {
    console.log(new Date().toLocaleTimeString() + ' - ' + data)
  }
  const debounceAjax = debounce(ajax, 1000)
  const throttleAjax = throttle(ajax, 1000)

  // const IntervalVal = setInterval(() => { debounceAjax('data') }, 500)
  // const IntervalVal = setInterval(() => { debounceAjax('data') }, 2000)
  const IntervalVal = setInterval(() => { throttleAjax('data') }, 500)

  ```

## 手写AJAX
  ```JavaScript
  var xhr = new XMLHttpRequest()
  xhr.open('GET','/XXX',true)
  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
      console.log(xhr.responseText)
    }
  }
  xhr.send()
  ```
## 手写一个 Promise
  ```JavaScript
  
  ```

## call, apply, bind 区别

  - apply() 方法调用一个具有给定this值的函数，以及以一个数组（或类数组对象）的形式提供的参数。
  - call()方法的作用和 apply() 方法类似，区别就是call()方法接受的是参数列表，而apply()方法接受的是一个参数数组
  - bind() 方法创建一个新的函数，在 bind() 被调用时，这个新函数的 this 被指定为 bind() 的第一个参数，而其余参数将作为新函数的参数，供调用时使用

## this 是什么

  - 函数的调用方式决定了 this 的值（运行时绑定）。this 不能在执行期间被赋值，并且在每次函数被调用时 this 的值也可能会不同
  - ES5 引入了 bind 方法来设置函数的 this 值
  - ES2015 引入了箭头函数，箭头函数不提供自身的 this 绑定

## 闭包/立即执行函数是什么

  - 立即执行函数：声明一个匿名函数马上调用这个匿名函数 创建一个独立的作用域 这个作用域里面的变量，外面访问不到 避免变量污染

  - 闭包 函数 A 返回了一个函数 B，并且函数 B 中使用了函数 A 的变量，函数 B 就被称为闭包
  ```JavaScript
  function A() {
    let a = 1
    function B() {
        console.log(a)
    }
    return B
  }
  ```

## async/await 怎么用,如何捕获异常？

  - async 关键字 这个函数总是返回一个 promise

  - await 关键字，它只在 async 函数内工作

  - await 不能在顶层代码运行
  ```JavaScript
  (async () => {
    let response = await fetch('/article/promise-chaining/user.json')
    let user = await response.json()
    ...
  })()
  ```

  - 要声明一个 class 中的 async 方法，只需在对应方法前面加上 async 即可

  - Error 处理
  ```JavaScript
  try{} catch {}

  .catch()
  ```

## 如何实现深拷贝？

## 不用 class 如何实现继承？用 class 又如何实现？

## 如何实现数组去重？

## Proxy
