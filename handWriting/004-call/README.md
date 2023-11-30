<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-30 15:10:02
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-30 17:28:16
 * @FilePath: \question-Interview\handWriting\004-call\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{手写call}$

### 思路分析
1. call 方法的定义

### 参考代码
1. $\color{#ff00ff}{call}$ 方法是一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。
    * 语法: ```fn.call(thisArg, arg1, arg2, ...)```
    * 作用: 让函数 fn 执行，执行时，函数体中的 this 使用指定的参数thisArg。
    * thisArg 在 fun 函数运行时，fun函数体中的 this 值 。
    * arg1, arg2, … 指定的参数列表。

2. $\color{#00a361}{call解析:}$ ```A.call(B, x, y)```
    * 让函数 call 执行, 两个作用
    * 改变函数 A 中的 this 指向, 使之指向 B
    * 让函数 A 执行, 把第二个参数及以后的参数传递给 函数 A , 即 A(x, y)
    ```
    const person = {
      name: "yyg"
    };
    function yygFn(x, y) {
      console.log(x, y);
      console.log(this.name);
    };
    yygFn.call(person, 4, 5); 
    //  4, 5
    //  yyg
    ```

3. $\color{#00a361}{开始实现: }$
    * $\color{#ee7b1d}{先改变 this 指向}$
    ```
    var name = "yyg";
    var person = {
      name: "code-name",
      say() {
        console.log(this.name)
      }
    };
    Function.prototype.yygCall = function(context) {
      var context = context || window;
      context.fn = this;
      context.fn();
      delete context.fn;
    };
    person.say.yygCall(window); //  yyg
    ```
    * $\color{#ee7b1d}{参数的传递(若干个)}$
    ```
    var name = "yyg";
    var person = {
      name: "code-name",
      say() {
        console.log("---", this.name);
        console.log("---", arguments);
      }
    };
    Function.prototype.yygCall = function(context) {
      var context = context || window, args = [], res = "";
      context.fn = this;
      for (let i = 1; i < arguments.length; i++) {
        args.push(`arguments[${i}]`)
      };
      res = eval(`context.fn(${args})`)
      delete context.fn;
      return res;
    };
    person.say.call(window, 1, 3, 4); 
    // yyg
    // Arguments(3) [1, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    person.say.yygCall(window, 1, 2, 3); 
    // yyg
    // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
    ```