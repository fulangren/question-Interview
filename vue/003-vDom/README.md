<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-29 16:57:59
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-29 17:22:58
 * @FilePath: \question-Interview\vue\003-vDom\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{谈谈对虚拟DOM的理解}$

### 思路分析
1. vDom 是什么
2. 使用 vDom 的好处
3. vDom 如何生成的，它又是如何成为真实 Dom
4. 在 diff 中的作用

### 回答参考
1. 虚拟 Dom 是一个虚拟的 dom 对象，本身是一个 $\color{#00a361}{javascript}$ 对象，它通过不同的结构属性描述一个视图结构。
2. 通过引入 vdom 的好处：
    - 将真实 dom 节点抽象成 vnode，减少直接操作 dom 的次数，从而可以提高性能。
    - 方便实现跨平台
3. vdom 如何生成的? 在 vue 中，我们会为组件编写模板 $\color{#ee7b1d}{-template}$ ，这个模板会被编译器 $\color{#ee7b1d}{-compiler}$编译为渲染函数，再接下来的挂载 （mounted）过程中调用 $\color{#00a361}{render}$ 函数，返回的对象就是虚拟DOM（vDom）；因为虚拟DOM 不是真实DOM，所以会在后续的 $\color{#00a361}{patch}$ 过程中转换为 DOM。
4. 挂载过程结束后，vue 程序进入更新流程，如果某些响应式数据发生了变化，就会引起组件重新 $\color{#00a361}{render}$，此时就会生成新的 vdom，和上次渲染结果 diff 就能得到变化的地方，从而转换为最小量的 dom 操作，高效更新视图。