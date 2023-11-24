<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-24 14:29:43
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-24 16:09:20
 * @FilePath: \question-Interview\vue\002-reactivity\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## 对vue响应式的理解
这个问题基本上每个面试上都会问到, 看别人总结的基本上没什么底气, 也经不起面试官的推敲。有空还是了解理解源码。

### 思路分析
1. 什么是响应式
2. 它能为我们带来什么好处
3. 为什么 vue 需要用到响应式
4. vue 的响应式是怎么实现的, 有什么优缺点
5. v3 中响应式的新变化

### 回答参考
1. 所谓的响应式是数据变化可以被侦测到并针对变化做出响应的机制
2. 以 vue 为例, 通过数据响应式 + 虚拟dom + patch 算法, 可以使我们只需要操作数据, 完全不用接触繁琐的dom操作, 从而提升开发效率, 降低开发难度
3. mvvm 框架中需要解决的一个核心点就是连接数据层和视图层, 通过数据驱动应用, 数据变化, 视图更新, 要做到这点就需要对数据做响应式处理, 这样一旦数据发生了变化就能立即做出更新处理。
4. vue2 中的数据响应式会根据**数据类型**来做不同的处理:
    * 如果是对象, 则采用 Object.defineProperty() 的方式定义数据拦截, 当数据被访问或发生改变时, 我们可以感知到并对此作出相应; 
    - 如果是数组, 则通过覆盖该数组原型的方法,扩展它的 7 个方法, 使这些方法可以额外的作出更新通知, 从而作出响应。
>vue2 中的响应式机制很好的解决了数据响应化的问题, 但在使用中存在一些缺点: 1) 初始化时的递归遍历会造成性能的损失; 2) 新增或者删除属性时需要用户使用 Vue.set/delete 这样特殊的api才能生效; 3) 不支持 es6 中新产生的 Map, Set 数据结
5. v3 为了解决v2 响应式中的一些问题, v3 重新编写了响应式的实现: 利用 ES6 中的 Proxy 机制代理要响应式的数据, 相对于 v2 的优势:
    * 编程体验一致, 不需要使用特殊的 api
    - 初始化性能和内存得到大幅改善 (v3 中数据访问/变化 才响应式)
    + 响应式的实现代码抽取出来为独立的 reactivity 包, 可以更灵活的使用它, 甚至可以不需要引入 vue 都可以体验。 

#### 传送门

vue2 响应式
https://github1s.com/vuejs/vue/blob/HEAD/src/core/observer/index.js#L135-L136

vue3 响应式
https://github1s.com/vuejs/core/blob/HEAD/packages/reactivity/src/reactive.ts#L89-L90

https://github1s.com/vuejs/core/blob/HEAD/packages/reactivity/src/ref.ts#L67-L68
