<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-12-01 14:19:24
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-12-01 14:44:23
 * @FilePath: \question-Interview\handWriting\006-Promise\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{手写 \ instanceof}$

### 思路分析
1. $\color{#ff00ff}{instanceof}$ 运算符用于判断构造函数的 $\color{#ee7b1d}{prototype}$ 是否出现在对象的原型链的任何位置。
2. 先获取类型的原型
3. 再获取对象的原型
4. 最后一直循环判断对象的原型是否等于类型的原型，直到对象的原型为 $\color{red}{null}$。

### 代码实现参考
```
function yygInstanceof(left, right) {
  if(typeof left !== "object" || left === null || typeof right !== "function") return false;
  
  let proto = Object.getPrototypeOf(left);  
  let prototype = right.prototype;

  while(true) {
    if(!proto) return false;
    if(proto === prototype) return true;
    proto = Object.getPrototypeOf(proto)
  }
}

console.log("11" instanceof String);  //  false
console.log(yygInstanceof("11",String));  //  false
console.log(yygInstanceof(new String("11"), String));  // true
```
