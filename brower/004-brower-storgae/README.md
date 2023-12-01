<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-12-01 11:17:57
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-12-01 13:30:41
 * @FilePath: \question-Interview\brower\004-brower-storgae\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## $\color{#ff00ff}{浏览器本地存储}$

### 思路分析
1. 有几种存储方式

### 回答参考
1. $\color{#00a361}{Cookie}$
    * 为了解决 服务端无法判断网路中的两个请求是否是同一个用户发起 的问题；
    * 一种纯文本文件，每次发起 HTTP 请求都会携带。
    * $\color{#00a361}{Cookie}$ 一旦创建成功，名称就无法修改；
    * $\color{#00a361}{Cookie}$ 是无法跨域名的；
        > 如果需要域名之间跨域共享Cookie，有两种方法：
        > 1) 使用Nginx反向代理 
        > 2) 在一个站点登陆之后，往其他网站写Cookie。服务端的Session存储到一个节点，Cookie存储sessionId
    * 每个域名下 $\color{#00a361}{Cookie}$ 的数量不能超过 $\color{red}{20}$ 个，每个 $\color{#00a361}{Cookie}$ 的大小不能超过 $\color{red}{4kb}$，生存时间由 $\color{#ee7b1d}{expires}$ 属性指定；
    * $\color{#00a361}{Cookie}$ 的应用场景：
        - Cookie和session结合使用，我们将sessionId存储到Cookie中，每次发请求都会携带这个sessionId，这样服务端就知道是谁发起的请求，从而响应相应的信息。
        - 可以用来统计页面的点击次数

2. $\color{#00a361}{LocalStorage}$
    * 有的时候我们存储的信息较大，Cookie 就不能满足我们的需求，这时候$\color{#00a361}{LocalStorage}$ 就派上用场了。
    * $\color{#00a361}{LocalStorage}$ 优点：
        - 在大小方面，LocalStorage的大小一般为5MB，可以储存更多的信息
        - $\color{#00a361}{LocalStorage}$ 是持久储存，并不会随着页面的关闭而消失，除非主动清理，不然会永久存在
        - 仅储存在本地，不像Cookie那样每次HTTP请求都会被携带
    * $\color{#00a361}{LocalStorage}$ 缺点：
        - 存在浏览器兼容问题，IE8以下版本的浏览器不支持
        - 如果浏览器设置为隐私模式，那我们将无法读取到LocalStorage
        - $\color{#00a361}{LocalStorage}$ 受到同源策略的限制，即端口、协议、主机地址有任何一个不相同，都不会访问
    * $\color{#00a361}{LocalStorage}$ 使用场景：
        - 有些网站有换肤的功能，这时候就可以将换肤的信息存储在本地的 $\color{#00a361}{LocalStorage}$ 中，当需要换肤的时候，直接操作 $\color{#00a361}{LocalStorage}$ 即可
        - 在网站中的用户浏览信息也会存储在 $\color{#00a361}{LocalStorage}$ 中，还有网站的一些不常变动的不涉及隐私个人信息等也可以存储在本地的 $\color{#00a361}{LocalStorage}$ 中

3. $\color{#00a361}{SessionStorage}$
    * $\color{#00a361}{SessionStorage}$ 主要用于临时保存同一窗口(或标签页)的数据，刷新页面时不会删除，关闭窗口或标签页之后将会删除这些数据。
    * $\color{#00a361}{SessionStorage}$ 也有同源策略的限制，但 $\color{#00a361}{SessionStorage}$ 只有在同一浏览器的同一窗口下才能够共享；
    * $\color{blue}{LocalStorage和SessionStorage都不能被爬虫爬取}$
    * $\color{#00a361}{SessionStorage}$ 使用场景：
        - 由于 $\color{#00a361}{SessionStorage}$ 具有时效性，所以可以用来存储一些网站的游客登录的信息，还有临时的浏览记录的信息。当关闭网站之后，这些信息也就随之消除了。

4. $\color{#00a361}{IndexedDB}$
    * $\color{#ee7b1d}{键值对储存：}$ $\color{#00a361}{IndexedDB}$ 内部采用对象仓库（object store）存放数据。所有类型的数据都可以直接存入，包括 JavaScript 对象。对象仓库中，数据以"键值对"的形式保存，每一个数据记录都有对应的主键，主键是独一无二的，不能有重复，否则会抛出一个错误。
    * $\color{#ee7b1d}{异步：}$ $\color{#00a361}{IndexedDB}$ 操作时不会锁死浏览器，用户依然可以进行其他操作，这与 $\color{#ee7b1d}{LocalStorage}$ 形成对比，后者的操作是同步的。异步设计是为了防止大量数据的读写，拖慢网页的表现。
    * $\color{#ee7b1d}{支持事务：}$ $\color{#00a361}{IndexedDB}$ 支持事务（transaction），这意味着一系列操作步骤之中，只要有一步失败，整个事务就都取消，数据库回滚到事务发生之前的状态，不存在只改写一部分数据的情况。
    * $\color{#ee7b1d}{同源限制：}$ $\color{#00a361}{IndexedDB}$ 受到同源限制，每一个数据库对应创建它的域名。网页只能访问自身域名下的数据库，而不能访问跨域的数据库。
    * $\color{#ee7b1d}{储存空间大：}$ $\color{#00a361}{IndexedDB}$ 的储存空间比 $\color{#ee7b1d}{LocalStorage}$ 大得多，一般来说不少于 $\color{red}{250MB}$ ，甚至没有上限。
    * $\color{#ee7b1d}{支持二进制储存：}$ $\color{#00a361}{IndexedDB}$ 不仅可以储存字符串，还可以储存二进制数据（ArrayBuffer 对象和 Blob 对象）。