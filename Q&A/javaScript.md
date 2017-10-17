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
 
