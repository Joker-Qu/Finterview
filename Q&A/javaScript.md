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

#### 统计给定数组中，各数出现的次数，返回 json 对象
```
function countNumber(arr) {
        var count = {}
        for(let item of arr){
            let key = `${item}`
            if (!count[key]){
                count[key] = 1
            }else {
                count[key]++
            }
        }
        return JSON.stringify(count)
    }
```
#### 字符串去重
```
function filter(str) {
        var arr = str.split('')
        var arr2 = []
        var count = {}
        for(let s of arr){
            var key = `${s}`
            if (!count[key]){
                count[key]=1
                arr2.push(s)
            }
        }
        return arr2.join('')
    }
```
#### Promise对象，嵌套try catch，内层嵌套错误捕获,怎样实现依次异步回调
#### js数据类型
六种原始数据类型:
- Boolean.  布尔值，true 和 false.
- null. 一个表明 null 值的特殊关键字。 JavaScript 是大小写敏感的，因此 null 与 Null、NULL或其他变量完全不同。
- undefined.  变量未定义时的属性。
- Number.  表示数字，例如： 42 或者 3.14159。
- String.  表示字符串，例如："Howdy"
- Symbol ( 在 ECMAScript 6 中新添加的类型).。一种数据类型，它的实例是唯一且不可改变的。
以及对象
#### 内存泄露 
不再用到的内存，没有及时释放，就叫做内存泄漏
JavaScript 在定义变量时就完成了内存分配
![参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management)
垃圾回收算法
- 引用记数 如果没有引用指向该对象（零引用），对象将被垃圾回收机制回收。但是该方法无法处理循环引用
- 标记清除 这个算法把“对象是否不再需要”简化定义为“对象是否可以获得”。JavaScript 中有个全局对象，浏览器中是 window。定期的，垃圾回收期将从这个全局对象开始，找所有从这个全局对象开始引用的对象，再找这些对象引用的对象...对这些活着的对象进行标记，这是标记阶段。清除阶段就是清除那些没有被标记的对象。

哪些情况会造成内存泄漏？
未清除的定时器、无意识的全局变量。
闭包：闭包并不会引起内存泄漏，只是由于IE9之前的版本对JScript对象和dom对象使用不同的垃圾收集，从而导致内存无法进行回收，这是IE的问题，所以闭包和内存泄漏没半毛钱关系。在低版本IE中虽然JavaScript对象通过标记清除的方式进行垃圾回收，但BOM与DOM对象却是通过引用计数回收垃圾的。
#### deepClone
```
function deepClone2(target) {
        if (typeof target === Object){
            var o = {}
            if (Object.prototype.toString.call(o) === '[object Array]'){
                o = []
            }
            for(let k in target){
                o[k] = deepClone(target[k])
            }
            return o
        }else {
            return target
        }
    }
```
#### 数组扁平化
```
//1
var result = []
    function filter(arr) {
        for(let item of arr){
            if (Array.isArray(item)){
                filter(item)
            }else {
                result.push(item)
            }
        }

    }
    filter([0,1,2,[3,4],5])
```
#### 写一个对象来满足A == '1'，然后问==和===的区别
对象和原始数据类型比较时，会先调用valueof方法，类型不同再调用toString方法
```
var A = {
        valueOf: function () {
            return 1
        }
    }
    console.log(A == '1')
```
#### 手写jsonp
```

    (function () {
        var foramtParams = function (data) {
            var arr = []
            for(var k in data){
                arr.push(encodeURIComponent(k)+'='+encodeURIComponent(data[k]))
            }
            return arr.join('&')
        }
        var jsonp = function (options) {
            options = options || {}
            if (!options.url || !options.callback) {
                throw new Error('参数不合法')
            }
            var callbackName = ('jsonp_'+Math.random()).replace(".","")
            var head = document.getElementsByTagName('head')[0]
            var params = ""
            if (options.data){
                options.data[options.callback] = callbackName
                params += foramtParams(options.data)
            }else {
                params += options.callback+'='+callbackName
            }
            var script = document.createElement('script')
            head.appendChild(script)
            window[callbackName] = function (json) {
                head.removeChild(script)
                clearTimeout(script.timer)
                window[callbackName] = null
                options.success && options.success(json)
            }
            script.src = options.url + '?' + params
            if (options.time){
                script.timer = setTimeout(function () {
                    window[callbackName] = null
                    head.removeChild(script)
                    options.fail && options.fail({message:"time out"})
                })
            }
        }
        window.jsonp = jsonp
    })()
    jsonp({
        url:"http://wwww.baidu.com",
        callback:'callback',
        data:{id:'1'},
        success:function (res) {
            console.log(res)
        },
        fail:function (err) {
            console.log(err)
        },
        time:10000
    })
    
```
#### 给出一个(010)111111，然后写代码来将这个模式的字符串转换为010-111111模式
```
function changestr(str) {
        return str.substring(1).split(')').join('-')
    }
    console.log(changestr('(010)111111'))
```
#### JavaScript的异步
![参考](https://segmentfault.com/a/1190000004322358)
异步：对io操作不用等待执行结果的调用方式
js是单线程，是指运行环境中负责解释和执行js代码的线程只有一个，可以叫他主线程。
但是还有处理ajax，dom事件等的其它线程，称为工作线程。

异步过程：主线程发起一个异步请求，相应的工作线程接收请求并告知主线程已收到(异步函数返回)；主线程可以继续执行后面的代码，同时工作线程执行异步任务；工作线程完成工作后，通知主线程；主线程收到通知后，执行一定的动作(调用回调函数)。

异步过程中，工作线程在异步操作完成后需要通知主线程。那么这个通知机制是怎样实现的呢？答案是利用消息队列和事件循环。
工作线程将消息放到消息队列，主线程通过事件循环过程去取消息。主线程只会做一件事情，就是从消息队列里面取消息、执行消息，再取消息、再执行。当消息队列为空时，就会等待直到消息队列变成非空。而且主线程只有在将当前的消息执行完成后，才会去取下一个消息。这种机制就叫做事件循环机制，取一个消息并执行的过程叫做一次循环。
消息就是对注册异步任务时添加的回调函数进行了包装。
异步过程中，工作线程在异步操作完成后需要通知主线程。那么这个通知机制是怎样实现的呢？答案是利用消息队列和事件循环。

#### promise封装ajax
```
function ajax(url,options) {
    return new Promise((resolve,reject) => {
        try {
            var data = options.data
            var type = options.type.toLowerCase();
            var params = []
            for (var k in options.params) {
                params.push(`${k}=${options.params[k]}`)
            }
            var req = XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject()
            if (type === 'get'){
                req.open(`${url}?${params.join('&')}`)
                req.send()
            }else {
                req.open(url)
                req.setRequestHeader('Content-type','application/x-www-form-urlencoded')
                req.send(params.join('&'))
            }
            req.onload = () => {
                if (req.status === 200 || req.status === 304){
                    resolve(req.responseText)
                }else {
                    reject(req.error)
                }
            }
        }catch (e){
            reject(e)
        }
    })
}
```
#### 手写一个NodeJS的fs.readFile方法的Promise封装
#### 如何使用ES6的generator函数来进行异步的调用
#### 箭头函数的特点
不绑定自己的this，arguments，不能用作构造函数
#### macro task micro task
JS 引擎会将所有任务按照类别分到这两个队列中，首先在 macrotask 的队列（这个队列也被叫做 task queue）中取出第一个任务，执行完毕后取出 microtask 队列中的所有任务顺序执行；之后再取 macrotask 任务，周而复始，直至两个队列的任务都取完。
全部代码(script)是一个macrotask,js先执行一个macrotask,执行过程中遇到(setTimeout, setInterval, setImmediate等)异步操作则创建一个macrotask,遇到(process.nextTick, Promises等)创建一个microtask,这两个queue分别被挂起.执行栈为空时开始处理macrotask,完成后处理microtask,直到该microtask全部执行完,然后继续主线程调用栈.

#### 排序，找出最大三个数
建堆，使用堆排序
堆的定义：堆是一颗完全二叉树。根节点的值大于左右子树，每一个子树也是堆，这样叫做大顶堆。
堆的调整：从最后一个非叶子节点开始，每次比较父节点，左孩子，右孩子的值，将最大的和父节点交换。
堆排序的时间复杂度为nlgn

#### 快速排序
```
// nlgn
function quicksort(arr) {
        if (arr.length <=1){
            return arr
        }
        var temp = arr[0]
        var left = []
        var right = []
        for(var i=1;i<arr.length;i++){
            if (arr[i]<temp){
                left.push(arr[i])
            }else {
                right.push(arr[i])
            }
        }
        return quicksort(left).concat([temp],quicksort(right))
    }
    console.log(quicksort([2,3,4,2,3,7,2,6,15]))
```

#### 继承的实现方式,详细问了创建实例对象的内部过程.
```
function People(name) {
        this.name = name
    }
    function Student(school) {
        People.call(this)
        this.school = school
    }
    Student.prototype.constructor = Student
    Student.prototype = Object.create(People.prototype)
```
#### 虚拟dom的原理和实现
在React中，render执行的结果得到的并不是真正的DOM节点，结果仅仅是轻量级的JavaScript对象，我们称之为virtual DOM。
虚拟dom性能优势归功于batching和diff算法
![参考](https://github.com/livoras/blog/issues/13)
虚拟dom的实现：
1. 用js对象表示dom。var VElement = function(tagName, props, children）
2. 比较两棵虚拟DOM树的差异.在深度优先遍历的时候，每遍历到一个节点就把该节点和新的的树进行对比。如果有差异的话就记录到一个对象里面。
但是要注意的是，因为tagName是可重复的，不能用这个来进行对比。所以需要给子节点加上唯一标识key，列表对比的时候，使用key进行对比，这样才能复用老的 DOM 树上的节点。
3. 对真实DOM进行最小化修改

#### es6模块的实现
![参考](https://ryerh.com/javascript/2016/03/27/babel-module-implementation.html)
用 Babel 把 ES6 的模块机制转换成 CommonJS 的形式.Babel 依然通过 exports 对象来输出模块内的引用，但是增加了一个特殊的 exports.default 属性用来实现 ES6 的默认输出对象。并且依然通过 require 来实现模块的加载。

#### 闭包
内部函数引用外部函数变量形成闭包。当我们需要在模块中定义一些变量，并希望这些变量一直保存在内存中但又不会“污染”全局的变量时，就可以用闭包来定义这个模块。