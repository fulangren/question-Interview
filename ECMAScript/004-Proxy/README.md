<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-28 15:17:34
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-28 15:45:48
 * @FilePath: \question-Interview\ECMAScript\004-Proxy\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{Proxy}$

### 思路分析
1. 对 $\color{red}{Proxy}$ 理解，
2. 与 $\color{red}{Object.defindProperty}$ 对比

### 回答参考
1. $\color{red}{Proxy}$ 可以理解为，在目前对象前设置一道拦截。外界对该对象的访问，都必须通过这层拦截，因此提供一种机制，可以对外界的访问进行过滤和改写，可以 “代理” 某些操作。
2. $\color{red}{Object.defineProperty}$ 使用的数据劫持：$\color{blue}{直接在对象上定义一个新属性，或者修改对象的现有属性，并返回该对象}$。
    * $\color{#00a361}{Vue \ 2.x}$ 利用 $\color{#00a361}{Object.defineProperty()}$，并把内部解耦成 $\color{#00a361}{Observer}$，$\color{#00a361}{Dep}$，并使用 $\color{#00a361}{Watch}$ 相连。
    * $\color{#00a361}{Vue \ 3.x}$ 改用 $\color{#ff00ff}{Proxy}$ 进行实现。
    #### $\color{#00a361}{Proxy}$ 和 $\color{#00a361}{Object.defineProperty}$ 的对比
    * $\color{#00a361}{Object.defineProperty}$
        - 只能监听对象，不能监听数组的变化，无法触发 $\color{#00a361}{push}$，$\color{#00a361}{pop}$，$\color{#00a361}{splice}$，
        $\color{#00a361}{shift}$，$\color{#00a361}{unshift}$，$\color{#00a361}{sort}$，$\color{#00a361}{reverse}$。
        - 必须遍历对象的每个属性
        - 只能劫持当前对象的属性，如果想深度劫持，必须深层遍历嵌套的对象。
    * $\color{#00a361}{Proxy}$
        - 可以监听对象而非属性。
        - 可以直接监听数组的变化