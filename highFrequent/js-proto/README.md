<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-27 10:40:26
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-28 09:25:14
 * @FilePath: \question-Interview\high-frequent\js-proto\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
# JS原型及原型链-构造函数
原型离不开构造函数，得先认识构造函数

## 构造函数

### 思路分析
1. 构造函数定义
2. 构造函数的优势
3. 构造函数的执行过程（new 操作符做了什么）
4. 构造函数的返回值
5. 构造函数为什么要用new关键字调用
6. 实例成员和静态成员
7. 和普通函数的区别

### 回答参考
1. 在 JS 中，任何使用 new 关键字来调用的函数，都叫构造函数【一般首字母大写】。
2. 使用对象字面量创建一些一系列同一类型的对象时，这些对象可能具有一些相似的 属性 和 方法，使用构造函数可降低代码冗余，提高代码复用率。
3. 具体见下：
```
const yygNew = (fn, ...args) => {
  let yygObj = {};  //  1. 创建一个空对象
  yygObj.__proto__ = fn.prototype;  //  2. 新对象的原型指向该构造函数的原型对象
  let result = fn.apply(yygObj, ...args); //  3.执行构造函数并将构造函数指向新对象
  return typeof result == 'object' ? result : yygObj; //  4.拿到构造函数的结果，判断是否是对象，如果是，直接返回，如果不是就返回新创建的对象
}
```
4. 构造函数的返回值默认返回this; 当return 基本数据类型时，最终返回this; 当return 复杂数据类型（对象）时，返回该对象。
5. 使用 new 关键字调用 this 对象指向构造函数生成的对象实例；不然直接调用，this 对象指向 window，不会默认返回任何对象。
6. 静态成员只能通过构造函数进行访问；实例成员之只能通过实例对象进行访问。
7.  | 普通函数 | 构造函数 |
    | :---: | :---: |
    | 不需要用new关键字调用 | 用new关键字调用 |
    | 函数内部不建议使用this | 函数内部可以使用this关键字 |
    | 可以 return 语句返回值 | 默认不用 return 返回值 |
    | 命名建议驼峰，首字母小写|首字母大写，与普通函数分开|
    |可以当构造函数用|可以当普通函数用|

## 谈谈原型和原型链
原型也可称是原型对象，原型与原型层层链接称为原型链

### 思路分析
1. 原型，原型链和构造函数的关系
2. 原型的作用
3. prototype 和 \__proto__
4. prototype 和 constructor
5. 原型链

### 回答参考
1. 每个构造函数（constructor）都有一个原型对象（prototype），原型对象都包含一个指向构造函数的指针，而实例（instance）都包含一个指向原型对象的内部指针。
2. 原型存在的意义就是组成原型链，原型链存在的意义就是继承，继承存在的意义就是属性共享：代码重用；可扩展【不同对象可能继承相同的属性，也可以定义只属于自己的属性】。
3. prototype 和 \__proto__有啥区别，又有啥关系呢
    * prototype：显示原型。
    * \__proto__：隐式原型。
    * 构造函数的 prototype 和其实例的 \__proto__ 指向的是同一个地方的。
    ```
    function Yyg(name) {
      this.name = name;
    }
    let yyg1 = new Yyg("嘤嘤怪1"); //  yyg1是构造函数 Yyg 的实例
    let yyg2 = new Yyg("嘤嘤怪2"); //  yyg2也是构造函数 Yyg 的实例
    console.log(yyg1.name, Yyg.prototype === yyg1.__proto__); // 嘤嘤怪1 true
    console.log(yyg2.name, Yyg.prototype === yyg2.__proto__); // 嘤嘤怪2 true
    ```
4. constructor 和 prototype 是成对的，你指向我，我指向你【我是你老公，你是我老婆，那我老婆的老公就是我自己】
    ```
    function fn() {}
    console.log(fn.prototype);  //  { constructor: fn }
    console.log(fn.prototype.constructor === fn); //  true
    ```
5. **原型链**
    * Yyg.prototype，它是构造函数 Yyg 的原型对象
    * Function.prototype，它是构造函数 Function 的原型对象
    原型对象本质还都是对象，既然是对象，本质一定是通过 new Object() 创建的，那就说明 Yyg.prototype 和 Function.prototype 是 构造函数 Object 的实例，就等于说 Yyg.prototype.\__proto__ 和 Fuction.prototype.\__proto__ 都是指向 Object.prototype。
    ```
    function Yyg() {}
    console.log(Yyg.prototype.__proto__ === Object.prototype);  //  true
    console.log(Function.prototype.__proto__ === Object.prototype); //  true
    ```
    * 那什么是原型链呢，\__proto__的路径就叫原型链，一直到原型链的终点 **null**。


### 备注：
![image](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/3/21/170fd29767b1485f~tplv-t2oaga2asx-jj-mark:3024:0:0:0:q75.png)