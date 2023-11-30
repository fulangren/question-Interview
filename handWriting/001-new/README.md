## $\color{#ff00ff}{手写new}$

### 思路分析
等同于问 $\color{#ff00ff}{new}$ 操作符做了啥/构造函数的执行过程
1. 创建一个新对象
2. 新对象的原型指向 构造函数 的原型对象
3. 执行构造函数并将构造函数指向新对象
4. 根据结果类型，判断是否是对象，如果是，直接返回，如果不是就返回新创建的对象

### 代码参考
```
function yygNew(fn, ...args) {
  let obj = {}; //  1
  obj.__proto__ = fn.prototype; //  2
  let res = fn.apply(obj, ...args); //  3
  return typeof res === "object" ? res : obj; //  4
}
```