<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-24 10:53:13
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-24 14:29:26
 * @FilePath: \question-Interview\vue\001-v-model\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## 双向绑定以及它的实现原理

### 题目分析：
双向绑定是vue的特色之一，开发中必然会用到的知识点，然而此题还问了实现原理，升级为深度考查。

### 思路分析：
1. 给出双绑定义
2. 双绑带来的好处
3. 在哪里使用
4. v-model 和 sync 修饰符有什么区别
5. v2 / v3 双绑的区别(实现原理)

## 回答参考：
1. vue 中双向绑定是一个指令 v-model；可以绑定一个动态值在视图上，同时视图层面的值发生变化时能改变该值。v-model是个语法糖，默认情况下时 :value 和 @input 的 结合体。
2. v-model 是个语法糖, 默认情况下相当于:value和@input。可以减少大量繁琐的事件处理代码, 提高开发效率。
3. v-model 一般在做表单项的使用，sync 用于在自定义组件中实现父子组件之间的双向绑定
4. 不同点可分为 **定义, 语法, 用法**
    * v-model 和 sync 都是 vue 中用于简化表单元素双向绑定的指令和修饰符；
    - v-model 在作用于标签只能有一个，而sync可以有一个或者多个；
    + 语法和用法的区别：
    ```
    <template>
      <input v-model="message" />
    </template>
    ```
    ```
    <!-- 父组件 -->
    <template>
      <div>
        <ChildComponent :childData.sync="parentData" />
      </div>
    </template>

    <!-- 子组件 -->
    <template>
      <div>
        <input :value="childData" @input="$emit('update:childData', $event.target.value)" />
      </div>
    </template>

    ```
5. 实现原理(移步002-reactivity)


