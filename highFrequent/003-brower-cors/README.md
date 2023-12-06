<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-12-06 16:56:37
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-12-06 17:21:42
 * @FilePath: \question-Interview\highFrequent\003-brower-cors\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{跨域解决方案}$

### 思路分析
跨域产生的原因 ---> 同源策略 ---> (协议 + 域名 + 端口)
同源策略限制行为： 
* Cookie、LocalStorage 和 IndexDB 无法读取
* DOM 和 JS 都不能获取
* 请求不能发送 

### 解决方案
1. $\color{#00a361}{JSONP \ 跨域}$
    * 利用 ```<script>```标签没有跨域限制
    * 只能发送 ```get``` 一种请求
    * 适合加载不同域名的js，css，img等静态资源

2. $\color{#00a361}{跨域资源共享 \ (CORS)}$
    * 允许浏览器向跨源服务器，发出```XMLHttpRequest```请求
    * 需要浏览器和服务器同时支持
    * 支持所有类型的HTTP请求，但浏览器```IE10```以下不支持

3. $\color{#00a361}{nginx \ 代理跨域}$
    * 搭建一个服务器，直接在服务器端请求HTTP接口，适合前后端分离的前端项目调后端接口

4. $\color{#00a361}{nodejs \ 中间件代理跨域}$
    * 同 ```nginx代理```一样，适合前后端分离的前端项目调后端接口

5. $\color{#00a361}{嵌入iframe}$

8. $\color{#00a361}{postMessage跨域}$
    * HTML5新特性，兼容性不是很好，只适用于主流浏览器和```IE10+```
    * 需要打开同域标签

9. $\color{#00a361}{WebSocket协议跨域}$
    * HTML5新特性，兼容性不是很好，只适用于主流浏览器和```IE10+```
    * 需要后端支持
