## $\color{#ff00ff}{手写apply}$

### 思路分析
1. apply 方式的作用
2. 与 call 区别

### 参考代码
1. 在 JS 中, $\color{#ff00ff}{apply}$ 和 $\color{#00a361}{call}$ 都是为了改变某个函数运行时的上下文。
2. 与  $\color{#00a361}{call}$ 区别：参数传递
```
var name = "yyg";
var person = {
  name: "code-name",
  say() {
    console.log("---", this.name);
    console.log("---", arguments);
  }
};
Function.prototype.yygApply = function(context, arr) {
  var context = context || window, args = [], res = "";
  context.fn = this;
  if(Array.isArray(arr)) {
    for (let i = 0; i < arr.length; i++) {
      args.push(`arr[${i}]`)
    };
    res = eval(`context.fn(${args})`)
    delete context.fn;
    return res;
  } else {
    return this;
  }
};
person.say.apply(window, [1,2,4]); 
// yyg
// Arguments(3) [1, 2, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
person.say.yygApply(window, [1, 2, 3]); 
// yyg
// Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```
