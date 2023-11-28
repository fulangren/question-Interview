<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-28 09:41:28
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-28 10:03:52
 * @FilePath: \question-Interview\ECMAScript\001-globalThis\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#FF00FF}{globalThis}$ 顶层对象

### 思路分析
1. globalThis 是什么?
2. globalThis 的作用

### 回答参考
1. 在 JS 中，都会存在一个顶层对象，它存在的意义提供全局作用环境（全局作用域），所有的代码都在这个环境中运行。但是顶层对象在各种实现中式不统一的，在浏览器环境指的式 window 对象，在 Node 指的是 global 对象。在 $\color{red}{ES5}$ 中，顶层对象的属性和全局变量是等价的。
2. 为了解决 $\color{#FF00FF}{1}$ 中问题
    * 为了保持兼容性， $\color{#FF00FF}{red}$ 声明 和 $\color{#FF00FF}{function}$ 声明的全局变量，依旧是顶层对象的属性；
    * let 命令，const 命令，class 命令声明的全局变量，不属于顶层对象的属性【从$\color{red}{ES6}$开始，全局变量将逐步与顶层对象的属性脱钩】。
    - 浏览器中，顶层对象是 window，但是 Node 和 Web Worker 没有window。
    - 浏览器和 Web Worker 里面，self 也是指向顶层对象，但是 Node 没有self。
    - Node 里面顶层对象是 global，但是其他环境都不支持。
    

3. **在任何环境下，globalThis 都是存在的，都可以从里面拿到顶层对象，指向全局环境的 this。**