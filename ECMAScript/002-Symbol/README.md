<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-28 11:12:45
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-28 13:33:45
 * @FilePath: \question-Interview\ECMAScript\002-Symbol\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{Symbol}$ 数据类型

### 思路分析
1. 定义
2. 相关api

### 回答参考
1. Symbol 是表示一种数据类型，继 $\color{#ff00ff}{undefined}$，$\color{#ff00ff}{null}$，$\color{#ff00ff}{Number}$，$\color{#ff00ff}{String}$，$\color{#ff00ff}{Boolean}$,$\color{#ff00ff}{Object}$ 之后。**表示独一无二的值。**
2. 相关 api 用法以及差异
    *  $\color{red}{Symbol.for()}$ 和 $\color{red}{Symbol()}$ 使用后会生成新的 Symbol，区别在于 $\color{red}{Symbol.for()}$ 会被登记在全局环境中供搜索，而 $\color{red}{Symbol()}$ 不会；也就是说 $\color{red}{Symbol.for()}$ 不会在每次调用就返回一个新的 $\color{#ff00ff}{Symbol}$ 类型的值，而是先检查给定的 key 是否存在，如果不存在才会新建一个值。调用 $\color{#ff8c75}{Symbol.for("yyg")}$ 10 次，每次都是返回同一个 $\color{#ff00ff}{Symbol}$ 值，但调用 $\color{#ff8c75}{Symbol("yyg")}$ 10 次，会返回 10 个 不同的 $\color{#ff00ff}{Symbol}$ 值。
    * $\color{red}{Symbol.iterator:}$ 指向该对象的默认遍历器方法。**对象在进行 for...of... 循环时，会调用到 $\color{#ff8c75}{Symbol.iterator}$** 方法，返回该对象的默认遍历器。
    * $\color{red}{Symbol.toStringTag:}$ 指向一个方法。在该对象上面调用 $\color{#ff8c75}{Object.prototype.toString}$ 方法，如果这个属性存在，就会出现在 $\color{#ff8c75}{toString}$ 方法返回的字符串中，表示对象的类型。换句话说，这个属性可以定制 $\color{#ff8c75}{[object \ Object]}$ 或 $\color{#ff8c75}{[object \ Array]}$ 后面的字符串。
    ```
    ({[Symbol.toStringTag]: "yyg"}.toString()); //  '[object yyg]'

    class Yyg {
      get [Symbol.toStringTag]() {
        return "yyg"
      }
    }
    let testYyg = new Yyg();
    Object.prototype.toString.call(testYyg);  //  '[object yyg]'
    ```