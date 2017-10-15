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
#### let块级作用域如何实现
其实就是进入{}后改变变量名
转换前：
```
let a1 = 1;
let a2 = 6;

{
    let a1 = 2;
    let a2 = 5;

    {
        let a1 = 4;
        let a2 = 5;
    }
}
a1 = 3;
转换后：

var a1 = 1;
var a2 = 6;

{
    var _a = 2;
    var _a2 = 5;

    {
        var _a3 = 4;
        var _a4 = 5;
    }
}
a1 = 3;
```
#### react diff算法
![参考](https://zhuanlan.zhihu.com/p/20346379)
普通树的diff算法复杂度是n的三次方，react通过大胆的假设将其变为n
具体来说有三个层次的diff算法
1. tree diff 树进行分层比较，两棵树只会对同一层次的节点进行比较。当发现节点已经不存在，则该节点及其子节点会被完全删除掉，不会用于进一步的比较。
2. component diff 不同组件直接替换不比较
3. element diff 对同一层级的同组子节点，添加唯一 key 进行区分




