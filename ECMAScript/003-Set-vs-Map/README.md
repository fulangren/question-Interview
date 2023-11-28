<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-28 13:46:32
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-28 15:13:04
 * @FilePath: \question-Interview\ECMAScript\003-Set-vs-Map\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#FF00FF}{Set - Map}$

### 思路分析
1. 两者的作用是什么，能做什么事
2. 相关的 api

### 回答参考
1. $\color{red}{Set}$ 成员的值都是唯一的，且是强类型的，会进行类型检查。
```
let yyg = new Set([1, "1", true, "true", 1, !false, "!fasle"]); // Set(5) {1, '1', true, 'true', '!fasle'}
```
* $\color{red}{Set}$ 可用来处理数组之间的交集，并集和差集。
```
let aYyg = new Set([1,2,3,4]), bYyg = new Set([3,4,7,8]);
//  交集
let intersect = new Set([...aYyg].filter(e=>bYyg.has(e))); //  Set(2) {3, 4}

// 并集
let union = new Set([...aYyg, ...bYyg]);  //  Set(6) {1, 2, 3, 4, 7, 8}

//  差集
let diff = new Set([...aYyg].filter(e=>!bYyg.has(e))); //  Set(2) {1, 2}
```
* $\color{red}{Map}$ 类似于对象，也是键值对的集合，但是 “键” 的范围不仅限于字符串，各种类型的值（包括对象）都可以作为键。
- $\color{red}{WeakSet}$ 和 $\color{red}{WeakMap}$ 所引用的对象都是弱引用，即垃圾回收机制不将 这个引用考虑在内。所以只要所引用的对象的其他引用都被清除，GC 就会释放该对象所占用的内存。也就是说，一旦不再需要，$\color{red}{WeakSet}$ 和 $\color{red}{WeakMap}$ 里面的键名对象和所对应的键值对会自动消失，不再需要手动删除引用。