<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-28 15:59:21
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-28 17:33:10
 * @FilePath: \question-Interview\ECMAScript\005-Reflect\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{Reflect}$
ECMAScript 为操作对象而提供的新 $\color{#00a361}{API}$

### 思路分析
1. $\color{#00a361}{Reflect}$ 作用是什么

### 回答参考
1. $\color{#00a361}{Reflect}$ 的作用
    * 将 $\color{#00a361}{Object}$ 对象的一些明显属于语言内部的方法（比如$\color{#00a361}{Object.defineProperty}$），放在 $\color{#00a361}{Reflect}$ 对象上。
    * 修改某些 $\color{#00a361}{Object}$ 方法返回的结果，让其变得更加合理。比如，$\color{#00a361}{Object.defineProperty(obj, name, desc)}$ 在无法定义属性时，会抛出一个错误（用try...catch...捕捉），而 $\color{#00a361}{Reflect.defineProperty(obj, name, desc)}$ 则会返回 $\color{red}{false}$。
    * 让 $\color{#00a361}{Object}$ 操作变成函数行为。某些 $\color{#00a361}{Object}$ 操作是命令式的，比如 $\color{#00a361}{name \ in \ obj}$，$\color{#00a361}{delete \ obj[name]}$，而 $\color{#00a361}{Reflect.has(obj, name)}$ 和 $\color{#00a361}{Reflect.defineProperty(obj, name)}$ 让他们变成了函数行为。
    * $\color{#00a361}{Reflect}$ 对象的方法与 $\color{#00a361}{Proxy}$ 对象的方法一一对应，只要是$\color{#00a361}{Proxy}$ 对象的方法，就能在 $\color{#00a361}{Reflect}$ 对象上找到对应的方法。这就让 Proxy 对象可以方便的调用对应的 Reflect 方法，完成默认行为，作为修改行为的基础。也就是说，不管 $\color{#00a361}{Proxy}$ 怎么修改默认行为，总能在 $\color{#00a361}{Reflect}$ 上获取默认行为。