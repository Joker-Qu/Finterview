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
