#### iframe加载完成后设置iframe高度
设置iframe的高度，使其等于内嵌网页的高度，从而看不出来滚动条和嵌套痕迹。
![iframe](http://caibaojian.com/iframe-adjust-content-height.html)
```
function setIframeHeight(iframe) {
  if (iframe) {
  var iframeWin = iframe.contentWindow || iframe.contentDocument.parentWindow;
  if (iframeWin.document.body) {
    iframe.height = iframeWin.document.documentElement.scrollHeight || iframeWin.document.body.scrollHeight;
    }
  }
};

window.onload = function () {
  setIframeHeight(document.getElementById('external-frame'));
};
```
如果嵌入的页面是跨域的，那么需要另一个页面作为代理进行设置
```
//a
<iframe src="http://www.b.com/c.html" id="Iframe" frameborder="0" scrolling="no" style="border:0px;"></iframe>
//c
<iframe id="c_iframe"  height="0" width="0"  src="http://www.a.com/agent.html" style="display:none" ></iframe>
<script type="text/javascript">
(function autoHeight(){
var b_width = Math.max(document.body.scrollWidth,document.body.clientWidth);
var b_height = Math.max(document.body.scrollHeight,document.body.clientHeight);
var c_iframe = document.getElementById("c_iframe");
c_iframe.src = c_iframe.src + "#" + b_width + "|" + b_height;  // 这里通过hash传递b.htm的宽高
})();
</script>
//agent
<script type="text/javascript">
    var b_iframe = window.parent.parent.document.getElementById("Iframe");
    var hash_url = window.location.hash;
    if(hash_url.indexOf("#")>=0){
        var hash_width = hash_url.split("#")[1].split("|")[0]+"px";
        var hash_height = hash_url.split("#")[1].split("|")[1]+"px";
        b_iframe.style.width = hash_width;
        b_iframe.style.height = hash_height;
    }
</script>
```
#### 水平垂直居中
1. flex
```
.parent {
    display: flex;
    justify-content: center; /* 水平居中 */
    align-items: center; /*垂直居中*/
  }
```
2. table
```
.parent {
    display: table-cell;
    text-align: center;//水平居中
    vertical-align: middle;//垂直居中
  }
  .child {
    display: inline-block;//防止块级元素宽度独占一行，内联元素可不设置
  }
```
3. absolute transform
```
.parent {
    position: relative;
  }
  .child {
    position: absolute;
    width:100px
    height:200px
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }
```
4. absolute margin
```
.parent {
    position: relative;
  }
  .child {
    position: absolute;
    width:100px
    height:200px
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    margin:-100px 0 0 -50px
  }
```
行内元素水平垂直居中：行内元素line－height等于父元素高度 父元素设置text-align:center即可

块级元素水平居中设置margin：0 auto即可

#### :和::的区别
单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素
新的在CSS3中引入的伪元素则不允许再支持旧的单冒号的写法。旧的css2中的before、after等伪元素仍然支持：写法。
#### nth-child和nth-type区别
p:nth-child(2)表示这个元素要是p标签，且是第二个子元素
p:nth-of-type(2)表示父标签下的第二个p元素
