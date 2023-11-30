<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-29 17:25:18
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-30 11:35:25
 * @FilePath: \question-Interview\ECMAScript\006-async\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{Async \ function}$

### 思路分析
1. async function 定义
2. async 出来的意义是什么
3. 函数返回什么，如果出错了怎么办
4. 和 await 表达式的结合用法

### 回答参考
1. $\color{#00a361}{async...await... 定义/简述：}$
    * async函数是使用async关键字声明的函数，是AsyncFunction构造函数的实例， 并且其中允许使用await关键字。
    * await关键字只在async函数内有效。如果在async函数体之外使用它，就会抛出语法错误 $\color{red}{SyntaxError}$ 。

2. $\color{#00a361}{async 出来的意义/目的}$
    * 可以用一种更简洁的方式写出基于Promise的异步行为，而无需刻意地链式调用promise；简化使用基于promise的API时所需的语法。
    * async/await的行为就好像搭配使用了生成器和promise

3. $\color{#00a361}{async函数介绍}$
    * 返回一个promise对象（promise对象的结果由async函数执行的返回值决定）
    * 如果一个async函数的返回值看起来不是promise，那么它将会被隐式地包装在一个promise中
    * 返回值是promise对象，那么async函数的返回值就是这个promise对象的成功或失败的值决定
    * async函数抛出错误，那么返回结果就是一个失败的promise对象

4. $\color{#00a361}{await表达式}$
    * await 必须写在async函数中
    * await右侧的表达式一般为promise对象
    >正常情况下，await 命令后是一个Promise 对象，返回该对象的结果；如果不是对象，那就直接返回对应的值。
    * await返回的是promise成功的值
    >如果是promise失败的结果, 整个async函数都会中断执行.
    * promise失败就会抛出异常，需通过try...catch捕获。

5. $\color{#00a361}{异步操作为什么要进行同步化}$
    * 希望程序异步执行，就是为了 “跳过” 阻塞，减少时间花销，或者避免回调地狱
    * 如果需要一系列的异步 “串行”，则需要保证信息/消息的顺序性时，就需要异步操作进行同步化，例如多个ajax的请求需要按照队列返回再依次处理，保证客户端的请求与响应顺序。
    >如果说 $\color{#ee7b1d}{Promise}$ 是为了解决回调地狱，那$\color{#ee7b1d}{async...await...}$ 主要就是为了将异步问题同步化。

6. $\color{#00a361}{async \ 实现原理}$
    * 是 $\color{#ee7b1d}{Generator}$ 的语法糖(将$\color{#ee7b1d}{Generator}$ 和 $\color{#ee7b1d}{自动执行器}$ 包装到一个函数中)
        - $\color{#ee7b1d}{Generator}$ 函数是一个普通函数, 但有两个特征
        > 1) function 关键字和函数名之间有个星号(*)
        > 2) 函数体内部使用 yield 表达式，定义不同的内部状态
        ```
        function* yygFn(x) {
          let y = yield x * 2;
          return y;
        }
        let res = yygFn(1);
        res.next(); //  { value: 2, done: false }
        res.next(); //  { value: undefined, done: true }
        ```
        > 3) $\color{#ee7b1d}{Generator}$ 函数, 会返回一个内部指针(遍历器) res 对象。
        > 4) next 方法的作用是分阶段执行 Generator 函数, 每次调用 next 方法,会返回一个对象, 表示当前阶段的信息(value 属性 和 done 属性)。value 属性是 yield 语句后面表达式的值, 表示当前阶段的值; done 属性是一个 Boolean 值, 表示 Generator 函数是否执行完毕。
