### 浏览器事件模型
事件发生分为三个阶段
1. 捕获
2. 目标
3. 冒泡
例如点击span元素 捕获阶段：window-document-body-...目标：span-冒泡：div-...body-document-window
- 捕获：从window逐步向下直到目标元素
- 目标：触发事件的元素
- 冒泡：逐级向上冒泡事件直到window

绑定在目标元素上的事件，不会遵循先捕获后冒泡的规则，而是哪种先绑定哪种先触发

e.target:真正触发事件的元素

e.currentTarget 事件绑定的元素

ie低版本的浏览器是用attachEvent，而高版本ie和标准浏览器用的是addEventListener

#### 实现bind函数
```
Function.prototype.bind2 = function (target,...params) {
        return () => {
            this.apply(target,params)
        }
    }
```
#### 类型转换
使用 == 进行比较时，可能会发生类型转换，先调用valueof方法，如果返回的不是原始类型，再调用toString方法
#### 判断数组
- Array.isArray(arr)
- Object.prototype.toString.call(arg) === '[object Array]'
#### 跨域
同源策略：协议、域名、端口相同我们认为是同源的，不同源时，会禁止ajax请求、dom操作和locolStorage、cookie等存储的获取。字体、img、script标签等不受影响。

跨域策略：
1. 代理转发
2. jsonp
3. cors
4. hash
5. webscoket
具体参考云笔记
