#### 统计字符串中字符出现的次数
```
function count(str) {
        const arr = str.split('')
        const result = {}
        for(let i of arr){
            if (!result[i]){
                result[i] = 1
            }else {
                result[i]++
            }
        }
        for(let k in result){
            console.log(`${k}:${result[k]}`)
        }
    }
    count('javascript')
```
用正则匹配指定字符串出现次数
```
return str.match(reg).length
```
#### websocket
WebSocket是持久化的h5协议。一旦WebSocket连接建立后，在客户端断开WebSocket连接或Server端中断连接前，不需要客户端和服务端重新发起连接请求。
#### XSS和CSRF
csrf 跨站请求伪造

攻击原理

用户登陆a网站产生cookie，然后访问危险网站b，b网站有指向a网站的危险链接，这个链接就是a的一个api接口，这个请求就携带cookie在用户不知道的情况下发出了

在业界目前防御 CSRF 攻击主要有三种策略：验证 HTTP Referer 字段；在请求地址中添加 token 并验证；在 HTTP 头中自定义属性并验证。

Referer 在 HTTP 头中有一个字段叫 Referer，它记录了该 HTTP 请求的来源地址。如果 Referer 是其他网站的话，则有可能是黑客的 CSRF 攻击，拒绝该请求。

请求地址中添加 token 并验证 djago <% csrf_token %>

xss 跨站脚本攻击

Content-Security-Policy、输入输出过滤转义两种。Content-Security-Policy是W3 org草案，主要就是用来定义页面可以加载哪些资源，减少XSS的发生，这样一来，从源头上杜绝了不可信源的XSS脚本加载的可能型。输入输出过滤转义主要指的是对变量的类型进行限制和针对字符串类型的数据把其中的特殊字符进行实体化转义，避免恶意脚本的执行。
#### http状态码
- 1 服务器收到请求
- 2 成功
- 3 重定向
  1. 301 永久移动
  2. 302 临时移动
  3. 304 资源未修改
- 4 客户端错误
  1. 400 请求格式错误
  2. 401 需要验证身份
  3. 403 禁止该请求
  4. 404 无法找到请求资源
- 5 服务端错误
  1. 501 服务器不支持该请求
  2. 502 网关或者代理服务器收到无效的请求
  3. 503 服务器过载
#### express特点
 简介灵活
#### nodejs内存泄露
#### Vuejs的生命周期
![](https://cn.vuejs.org/images/lifecycle.png)
#### 组件化思想
1. “资源高内聚”—— 组件资源内部高内聚，组件资源由自身加载控制
2. “作用域独立”—— 内部结构密封，不与全局或其他组件产生影响 
3. “自定义标签”—— 定义组件的使用方式
4. “可相互组合”—— 组件正在强大的地方，组件间组装整合
5. “接口规范化”—— 组件接口有统一规范，或者是生命周期的管理
#### node异步非阻塞 I/O 底层实现原理
