<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-30 17:53:02
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-12-01 10:55:40
 * @FilePath: \question-Interview\vue\004-nextTick\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{nextTick实现原理}$

### 思路分析
1. vue异步更新策略
2. 说出vue是怎么通过异步、批量的方式更新以提高性能的
3. 源码中实现

### 回答参考
1. nextTick是Vue提供的一个全局API，由于vue的异步更新策略导致我们对数据的修改不会立刻体现在dom变化上，此时如果想要立即获取更新后的dom状态，就需要使用这个方法
2. Vue 在更新 DOM 时是异步执行的。只要侦听到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 watcher 被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际 (已去重的) 工作。Vue 在内部对异步队列尝试使用原生的 Promise.then、MutationObserver 和 setImmediate，如果执行环境不支持，则会采用 setTimeout(fn, 0) 代替。
3. 当我们想在修改数据后立即看到dom执行结果就需要用到nextTick方法。（比如我在干什么的时候就会使用nextTick，传一个回调函数进去，在里面执行dom操作即可。）
4. $nextTick() 返回一个 Promise 对象，所以你可以使用新的 ES2017 async/await 语法完成相同的事情：
```
methods: {
  updateMessage: async function () {
    this.message = '已更新'
    console.log(this.$el.textContent) // => '未更新'
    await this.$nextTick()
    console.log(this.$el.textContent) // => '已更新'
  }
}
```
5. 源码中：
    * 修改一个数据，组件对应的watcher会尝试入队:
    ```
      queue.push(watcher)
    ```
    * 并使用nextTick方法添加一个flushSchedulerQueue回调：
    ```
    nextTick(flushSchedulerQueue)
    ```
    * flushSchedulerQueue被加入callbacks数组：
    ```js
    callbacks.push(() => {
      if (cb) {
        try {
          cb.call(ctx) // cb就是加入的回调
        } catch (e) {
          handleError(e, ctx, 'nextTick')
        }
      } 
    })
    ```
    * 然后以异步方式启动
    ```js
    if (!pending) {
      pending = true
      timerFunc()
    }
    ```
    * timerFunc的异步主要利用Promise等微任务方式实现
    ```js
    let timerFunc
    
    if (typeof Promise !== 'undefined' && isNative(Promise)) {
      const p = Promise.resolve()
      // timerFunc利用p.then向微任务队列添加一个flushCallbacks
      // 会异步调用flushCallbacks
      timerFunc = () => {
        p.then(flushCallbacks)
      }
      isUsingMicroTask = true
    }
    ```
    * flushCallbacks遍历callbacks，执行里面所有回调
    ```js
    function flushCallbacks () {
      pending = false
      const copies = callbacks.slice(0)
      callbacks.length = 0
      for (let i = 0; i < copies.length; i++) {
        copies[i]()
      }
    }
    ```
    * 其中就有前面加入的flushSchedulerQueue，它主要用于执行queue中所有watcher的run方法，从而使组件们更新
    ```js
    for (index = 0; index < queue.length; index++) {
      watcher = queue[index]
      watcher.run()
    }
    ```