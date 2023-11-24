<!--
 * @Author: fulangren 1746575462@qq.com
 * @Date: 2023-11-24 16:33:05
 * @LastEditors: fulangren 1746575462@qq.com
 * @LastEditTime: 2023-11-24 17:59:40
 * @FilePath: \question-Interview\brower\001-http-cache\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
## 对 http 缓存的理解
一个高频出现的面试题，一个强缓存、协商缓存简单几句话就能概括的缓存机制，一个所有前端页面都需要用到却又极少被关注的功能
缓存是为了重复使用而被存储的，可以减少浏览器和服务器之间的通信次数，降低网络延迟，加速页面加载，提升用户体验。不但能使网页打开更快，还能减少服务器压力。

### 思路分析
1. http 缓存的作用
2. 缓存方式有哪些，如何判断是缓存方式
3. 如何判断是缓存方式
4. 

### 回答参考
1. 缓存时为了可以重复使用而被存储的，可以减少浏览器和服务器之间的通信次数，降低网络延迟，加速页面加载，提升用户体验，可以时页面打开的更快，还能减少服务器的压力。
2. 缓存方式可分为**强缓存**和**协商缓存**
    * 命中**强缓存**： Expires 和 Cache-Control
        + Expires 是给出的缓存过期的**绝对时间(时间点)**，超过这个时间，缓存资源过期（有可能服务器的时间和客户端的时间不一致导致缓存时间不如预期）。
        + Cache-Control 用于控制缓存的行为，可以组合多种指令(指令之间可通过 "；"分隔)，常用的指令：private/public，max-age，s-maxage，no-cache/no-store。
            - private：资源只能被客户端缓存
            - public：资源可以被客户端、代理服务器、公共缓存服务器缓存
            - max-age：给出缓存的相对时间（时间段），单位为秒，即得到响应之后多少秒后过期，和 Expires 同时出现，max-age 优先级高于 Expires。
            - s-maxage：对公共缓存/代理服务器生效，表示资源在公共/代理服务器中缓存的相对时间。
            - no-cache：表示客户端每次使用缓存资源前必须像服务器确认其有效性
            - no-store：不缓存资源
    >sdad


