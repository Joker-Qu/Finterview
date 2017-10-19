#### 浏览器缓存
![](http://www.alloyteam.com/wp-content/uploads/2012/03/http-header1.png)
![参考](http://www.alloyteam.com/2012/03/web-cache-2-browser-cache/#prettyPhoto)
cache-control和expires都可以设置资源的有效期，但是cache－control有更多的设置项，并且优先级比expires高

last－modify和etag都是响应头，分别告知资源的最后修改时间和唯一标示符。
#### 负载均衡
负载均衡（Load Balance），意思是将负载（工作任务，访问请求）进行平衡、分摊到多个操作单元（服务器，组件）上进行执行。
软件负载均衡解决方案是指在一台或多台服务器相应的操作系统上安装一个或多个附加软件来实现负载均衡
硬件负载均衡解决方案是直接在服务器和外部网络间安装负载均衡设备，这种设备通常称之为负载均衡器，
#### web性能优化
#### 服务端渲染的好处
首屏速度快、seo
#### dns解析
定义：把域名“翻译”成了相应的IP地址
过程：比如输入www.qq.com 操作系统会检查本地host文件里面有没有对应的关系，有直接返回。否则会去查找本地dns解析器缓存。然后再去查本地dns服务器，若仍然没有，会把请求发给根dns，根服务器返回管理.com的顶级服务器ip。然后本地服务器会发请求给该顶级服务器进行查找，顶级服务器找不到就去找管理qq.com的服务器并重复之前过程直到找到该ip地址。从客户端到本地DNS服务器是属于递归查询，而DNS服务器之间就是的交互查询就是迭代查询。

dns劫持就是通过劫持了DNS服务器，修改域名的解析结果，导致用户对特定的网址不能访问或访问的是假网址。预防措施个人来说就是修改路由器帐号密码，公司则提供备用域名。
#### http2
#### HTTP协议中常用的报文头
常用的HTTP请求头

协议头	说明	示例	状态
- Accept	可接受的响应内容类型（Content-Types）。	Accept: text/plain	固定
- Accept-Charset	可接受的字符集	Accept-Charset: utf-8	固定
- Accept-Encoding	可接受的响应内容的编码方式。	Accept-Encoding: gzip, deflate	固定
- Accept-Language	可接受的响应内容语言列表。	Accept-Language: en-US	固定
- Cache-Control	用来指定当前的请求/回复中的，是否使用缓存机制。	Cache-Control: no-cache	固定
- Connection	客户端（浏览器）想要优先使用的连接类型	Connection: keep-alive
- Cookie	由之前服务器通过Set-Cookie（见下文）设置的一个HTTP协议Cookie	Cookie: $Version=1; Skin=new;	固定：标准
- Content-Length	以8进制表示的请求体的长度	Content-Length: 348	固定
- Content-Type	请求体的MIME类型 （用于POST和PUT请求中）	Content-Type: application/x-www-form-urlencoded	固定
- Host	表示服务器的域名以及服务器所监听的端口号。如果所请求的端口是对应的服务的标准端口（80），则端口号可以省略。	
常用的HTTP响应头

- Access-Control-Allow-Origin	指定哪些网站可以跨域源资源共享	Access-Control-Allow-Origin: *	临时
- Allow	对于特定资源的有效动作;	Allow: GET, HEAD	固定
- Cache-Control	通知从服务器到客户端内的所有缓存机制，表示它们是否可以缓存这个对象及缓存有效时间。其单位为秒	Cache-Control: max-age=3600	固定
- Content-Encoding	响应资源所使用的编码类型。	Content-Encoding: gzip	固定
- Content-Language	响就内容所使用的语言	Content-Language: zh-cn	固定
- Content-Length	响应消息体的长度，用8进制字节表示	Content-Length: 348	固定
- ETag	对于某个资源的某个特定版本的一个标识符，通常是一个 消息散列	ETag: "737060cd8c284d8af7ad3082f209582d"	固定
- Expires	指定一个日期/时间，超过该时间则认为此回应已经过期	Expires: Thu, 01 Dec 1994 16:00:00 GMT	固定: 标准
- Last-Modified	所请求的对象的最后修改日期(按照 RFC 7231 中定义的“超文本传输协议日期”格式来表示)	Last-Modified: Dec, 26 Dec 2015 17:30:00 GMT	固定
#### HTTPS的原理
