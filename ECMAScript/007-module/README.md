<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-12-01 16:52:30
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-12-01 17:36:29
 * @FilePath: \question-Interview\ECMAScript\007-modules\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{ES6模块化}$
模块化编程的核心思想是将代码分为独立的部分，每个部分都负责一个特定的功能或任务。每个模块都有自己的作用域，内部的变量和函数，不会和其他模块发生冲突。

### 思路分析
模块是一种组织代码的方式，它允许你将相关的功能和变量组合在一起，形成一个独立的单元。这个单元可以被其他部分引用，就像是建筑中的一个组件可以被多次使用。

### 回答参考
1. $\color{#00a361}{export}$ 和 $\color{#00a361}{import}$
    * $\color{#ee7b1d}{export:}$ 用于将模块中的函数，变量，类等导出，使其在其他模块中可用。可以用 ```export``` 关键字来导出命名导出或默认导出。
    * $\color{#ee7b1d}{import：}$ 用于导入其他模块中导出的函数，变量等。可以使用 ```import``` 关键字来导入命名导出或默认导出。
2. $\color{#00a361}{默认导出}$ 和 $\color{#00a361}{命名导出}$
    * $\color{#ee7b1d}{命名导出：}$通过 ```export``` 关键字导出多个函数、变量或类，然后在导入模块中使用相同的名称来引入它们。
    ```
    // math.js
    export function add(a, b) {
      return a + b;
    }

    export function subtract(a, b) {
      return a - b;
    }

    // main.js
    import { add, subtract } from './math.js';
    console.log(add(5, 3)); // 8
    console.log(subtract(5, 3)); // 2
    ```
    * $\color{#ee7b1d}{默认导出：}$通过 ```export default``` 关键字导出一个默认值，通常是一个函数、类或对象。在导入模块中，可以使用不同的名称来引入默认导出。
    ```
    // math.js
    export default function multiply(a, b) {
      return a * b;
    }

    // main.js
    import myMultiplier from './math.js';
    console.log(myMultiplier(5, 3)); // 15
    ```


### $\color{red}{浏览器中的 \ ES \ Modules}$
```ES Modules```不仅在 ```Node.js```中可用，它们也可以在现代浏览器中使用，这为前端开发带来了更多模块化的可能性。
* $\color{#00a361}{在HTML中引入ES Modules}$
>要在浏览器中使用```ES Modules```，你可以在HTML文件中使用\<script>标签，并将type属性设置为module。这告诉浏览器加载的脚本是ES Module。
```
<script type="module" src="main.js"></script>
```
* $\color{#00a361}{异步加载模块}$
>可能需要异步加载模块，以避免阻止页面的加载。你可以使用```import()```函数来实现异步加载，使得在需要时按需加载模块成为可能，提高了页面性能
```
import('./lazyModule.js')
  .then(module => {
    // 使用异步加载的模块
  }).catch(error => {
    console.error(error);
  });
```
* $\color{#00a361}{跨域加载}$
>```ES Modules```也支持跨域加载。你可以从其他域的服务器加载模块，只要 $\color{red}{服务器允许跨域请求}$。这为构建跨域应用程序提供了更多的可能性。
```
import('https://www.baidu.com/xxxx.js')
  .then(module => {
    // 使用远程加载的模块
  }).catch(error => {
    console.error(error);
  });
```