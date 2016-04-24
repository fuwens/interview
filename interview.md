## 面试总结
### 1、手写深拷贝（问：说一下可以吗？回答：必须手写出来。-。-）
深拷贝的主要考察这几个点：数据类型的检测、递归。
参考代码：
```js
function clone(obj){
    var o;
    if(typeof(obj) !== "object" || obj === null){return obj};
    if(obj instanceof(Array)){
        o=[];
        for(var i=0;i<obj.length;i++){
            if(typeof(obj[i]) === "object" && obj[i] !== null){
                o[i]=arguments.callee(obj[i]);
            }else{
                o[i]=obj[i];
            }
        }
    }else{
        o={};
        for(var key in obj){
            typeof(obj[i] === "object" && obj[i] !== null){
                o[i]=arguments.callee(obj[i]);
            }else{
                o[i]=obj[i];
            }
        }
    }
    return  o;
};
```

### 2、数据类型判断
typeof 和 instanceof 
typeof是一种操作符，用来检测给定变量的数据类型。它的返回值有：undefined、 boolean、 string、 number、 object、 function。
注：null被认为是一个空的对象引用，所以返回也是object
instanceof也是一种操作符，因为用typeof检测引用类型的数据时候，返回的都是object，所以我们用instanceof来检测检测某个值是什么类型的对象或者用于判断一个变量是否某个对象的实例。

### 3、如何让一个图片上下居中显示（）不知道图片的宽高
一般情况下都是知道盒子大小以及图片的宽高的，这种情况是利用定位的方式，如下
```css
    .box{
        width:400px;
        height:400px;
        position:relative;
    }
    img{
        width:100px;
        height100px;
        position:absolute;
        top:50%;
        left:50%;
        margin-left:-50px;
        margin-top:-50px;
    }
```
在不知道img的宽高的情况下我们可以用table-cell的方式，display:table-cell属性指让标签元素以表格单元格的形式呈现。
还有一种方式是利用flex布局。

### 4、window.onload 和 document.ready的区别
document.ready是dom树加载完成后就触发，而window.onload是dom树加载完并且其他资源也加载完（例如图片资源）。
所以document.ready要比window.onload先执行。

### 5、如何在iphone下画1px的直线
a. transform: scale(0.5)
```css
    .after-scale{
        position: relative;
    }
    .after-scale:after{
        content:"";
        position: absolute;
        bottom:0px;
        left:0px;
        right:0px;
        border-bottom:1px solid #c8c7cc;
        -webkit-transform:scaleY(.5);
        -webkit-transform-origin:0 0;
    }
```
b. box-shadow
```css
    -webkit-box-shadow:0 1px 1px -1px rgba(0, 0, 0, 0.5);
```
c.background-image
```css  
    .border {
          background-image:linear-gradient(180deg, red, red 50%, transparent 50%),
          linear-gradient(270deg, red, red 50%, transparent 50%),
          linear-gradient(0deg, red, red 50%, transparent 50%),
          linear-gradient(90deg, red, red 50%, transparent 50%);
          background-size: 100% 1px,1px 100% ,100% 1px, 1px 100%;
          background-repeat: no-repeat;
          background-position: top, right top,  bottom, left top;
          padding: 10px;
      }
```

### 6、dataset 和 classList
HTML5中我们可以使用data-前缀设置我们需要的自定义属性，来进行一些数据的存放。然后通过dataset去获取值。
```html
    <div id="day2-meal-expense" 
      data-drink="coffee" 
    </div>
    var expenseday2 = document.getElementById('day2-meal-expense');  
    var typeOfDrink = expenseday2.dataset.drink;
```
在HTML5 API里，页面DOM里的每个节点上都有一个classList对象，程序员可以使用里面的方法新增、删除、修改节点上的CSS类.
```js
    myDiv.classList.add('myCssClass');
    myDiv.classList.remove('myCssClass');
    myDiv.classList.toggle('myCssClass'); //现在是增加
    myDiv.classList.toggle('myCssClass'); //现在是删除
    myDiv.classList.contains('myCssClass'); //returns true or false
```

### 7、数组去重
```js
    function unique (arr) {
        var json={},res=[];
        for(var i=0;i<arr.length;i++){
            if(!json[arr[i]]){
                json[arr[i]] = true;
                res.push(arr[i]);
            }
        }
        return res;
    }
```


### 8、js实现原型继承
```js
    var obj ={
        name:'mzhuang'
        say:function(){
            console.log(this.name);
        }
    }
    var b = clone(obj);
    b.name = "bbbbb";
    console.log(b.say()) //bbbbb
    function clone(obj){
        var F= function(){};
        F.protopyte=obj;
        renturn new F();
    }
```
### 9.js实现类式继承
```js
    function Person(){
        this.name="Person";
    }
    Person.protopyte.say=function(){
        console.log(this.name);
    }
    function Man(){
        Person.call(this);
        this.name ="Man";
    }
    Man.protopyte = new Person();
    Man.protopyte.constructor =Man;

    var aMan = new Man();
    console.log(aMan.say()) //Man

```

### 10、浏览器的事件模型
事件冒泡和事件捕获。https://segmentfault.com/a/1190000003482372
事件的绑定和事件对象event,阻止事件冒泡和取消默认行为。
addEventListener标准下绑定事件，ie下attachEvent.
e.stopPropagation()阻止事件冒泡  
e.preventDefault()取消事件的默认行为
ie:
window.event.cancelBubble = true;//停止冒泡
window.event.returnValue = false;//阻止事件的默认行为

### 11、找出一个字符串中出现最多的字符
```js
    var str = "fssdhsd";
    var obj={};
    for (var i = 0; i < str.length; i++) {
        if(obj[str.charAt(i)]){
            obj[str.charAt(i)]++;
        } else{
            obj[str.charAt(i)] = 1;
        }
        
    }
    console.log(obj);
    var tem = 0;
    var val = null;
    for(var key in obj){
        if(obj[key] > tem ){
            val = key;
            tem = obj[key]
        }
    }
    console.log("出现最多的是："+val+"，总共出现"+tem+"次")

```

### 12、实现一个事件代理
利用事件的冒泡机制，在需要绑定事件的父元素上绑定事件，然后通过event.target来判断点击在哪个元素，然后执行相应的事件
```html
    <ul class="list">
        <li>111111</li>
        <li>222222</li>
        <li>333333</li>
        <li>444444</li>
        <li>555555</li>
        <li>666666</li>
    </ul>
```

```js
    window.onload = function(){
                //console.log(document.querySelectorAll('.list'));
                function getEventTarget(e){
                    var e= e || window.event;
                    return e.target || e.srcElement;                
                }
                var ul = document.querySelector('.list');
                ul.onclick= function(e){
                    var target= getEventTarget(e);
                    if(target.tagName.toLowerCase() == 'li'){
                        alert(target.innerHTML)
                    }   
                }
            }
```

### 13、实现一个快速排序
```js
    function quickSort(arr){
        if(arr.length <= 0 ){return arr;}
        var pivotIndex = Math.floor(arr.length/2);
        var pivot = arr.splice(pivotIndex,1)[0];  //取得中间值
        var left =[];
        var right =[];
        for (var i = 0; i < arr.length; i++) {
            if(arr[i]<pivot){
                left.push(arr[i]);
            }else{
                right.push(arr[i]);
            }
        }
        return arguments.callee(left).concat([pivot],arguments.callee(right))

    };
```

### 14、你用过的那些自动化处理工具
gulp、grunt
gulp是一个基于流的自动化构建工具。
gulp.src 输出（Emits）符合所提供的匹配模式（glob）或者匹配模式的数组（array of globs）的文件。
gulp.watch 监视文件，并且可以在文件发生改动时候做一些事情。
gulp.dest 能被 pipe 进来，并且将会写文件。
gulp.task  //定义一个使用 Orchestrator 实现的任务（task）。

### 15、css伪类和伪元素
a.伪类

    :link
    伪类将应用于未被访问过的链接，与:visited互斥。
    :hover
    伪类将应用于有鼠标指针悬停于其上的元素。
    :active
    伪类将应用于被激活的元素，如被点击的链接、被按下的按钮等。
    :visited
    伪类将应用于已经被访问过的链接，与:link互斥。
    :focus
    伪类将应用于拥有键盘输入焦点的元素。
    :first-child
    伪类将应用于元素在页面中第一次出现的时候。
    :lang
    伪类将应用于元素带有指定lang的情况。

b.伪元素

    :first-letter
    伪元素的样式将应用于元素文本的第一个字（母）。
    :first-line
    伪元素的样式将应用于元素文本的第一行。
    :before
    在元素内容的最前面添加新内容。
    :after
    在元素内容的最后面添加新内容。

### 16、css3的动画
Transition 语法：transition: property duration timing-function delay;
Animation 语法：animation: name duration timing-function delay iteration-count direction; 通过@keyframes定义动画。
Transform  语法: transform: rotate() / skew() / scale() / translate(,) ，旋转/倾斜/缩放/位移

### 17、js中的call,apply,callee,caller
1.call 方法
调用一个对象的一个方法，以另一个对象替换当前对象。
Function.call([thisObj[,arg1[, arg2[,   [,.argN]]]]])
参数
thisObj

可选项。将被用作当前对象的对象。

arg1, arg2,  , argN

可选项。将被传递方法参数序列。

说明
call 方法可以用来代替另一个对象调用一个方法。call 方法可将一个函数的对象上下文从初始的上下文改变为由 thisObj 指定的新对象。

如果没有提供 thisObj 参数，那么 Global 对象被用作 thisObj。

要求
版本 5.5

以obj1.method1.call(obj2,argument1,argument2,...)为例：
call方法的调用者：一个对象的方法（在js里面方法/函数也是对象），调用者为，obj1.method1
call方法的参数：一个新对象（obj2），这个对象的作用是“拦截”对象obj1，来运行本来属于obj1的method方法；而 argument1,argument2,...就是给method传递参数了
call方法的结果：obj1.method1.call(obj2,argument1,argument2,...)等价于：
obj2.method1(argument1,argument2,...)
call方法的作用：obj1.method方法得到重用、共享，有new的特效，实现继承

2.apply 方法
Function.apply(obj,args)方法能接收两个参数
obj：这个对象将代替Function类里this对象
args：这个是数组，它将作为参数传给Function（args-->arguments）
apply和call,这两个方法基本上是一个意思
区别在于 call 的第二个参数可以是任意类型，而apply的第二个参数必须是数组，也可以是arguments

3.callee 方法
返回正被执行的 Function 对象，也就是所指定的 Function 对象的正文。
［function.］arguments.callee
可选项 function 参数是当前正在执行的 Function 对象的名称。
说明
callee 属性的初始值就是正被执行的 Function 对象。
callee 属性是 arguments 对象的一个成员，它表示对函数对象本身的引用，这有利于匿名函数的递归或者保证函数的封装性。还有需要注意的是callee拥有length属性，这个属性有时候用于验证还是比较好的。arguments.length是实参长度，arguments.callee.length是形参长度，由此可以判断调用时形参长度是否和实参长度一致。

4.caller 方法
返回一个对函数的引用，该函数调用了当前函数。
functionName.caller
functionName 对象是所执行函数的名称。
说明
对于函数来说，caller 属性只有在函数执行时才有定义。 如果函数是由 Javascript 程序的顶层调用的，那么 caller 包含的就是 null 。

### 18、js DOM操作
http://group.cnblogs.com/topic/39811.html
元素节点操作的方法
a.创建节点，createElement创建元素，createTextNode创建文本节点
b.插入节点，appendChild，inserBefore(a,b)
c.替换和删除节点，repalceChild、removeChild.
d.节点属性， 
    firstChild:第一个子节点
    lastChild:最后一个子节点
    childNodes:子节点集合
    nextSibling:下一个兄弟节点
    previousSibling:上一个兄弟节点
    parentNode:父节点
e.createDocumentFragment() 创建文档片段。

### 19、node如何避免回调地狱

模块化：将回调函数分割为独立的函数
使用Promises
使用yield来计算生成器或Promise

### 20、使用NPM有哪些好处？
通过NPM，你可以安装和管理项目的依赖，并且能够指明依赖项的具体版本号。 对于Node应用开发而言，你可以通过package.json文件来管理项目信息，配置脚本， 以及指明项目依赖的具体版本。

### 21、css3 box-siziong属性
box-sizing属性可以为三个值之一：content-box（default），border-box，padding-box。

content-box：border和padding不计算入width之内

padding-box：padding计算入width内

border-box：border和padding计算入width之内，其实就是怪异模式了

### 22、cookies\sessionStorage\localStorage
    cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下。存储大小限制也不同，cookie数据不能超过4k，同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如会话标识。sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。作用域不同，sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面；localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。Web Storage 支持事件通知机制，可以将数据更新的通知发送给监听者。Web Storage 的 api 接口使用更方便。

### 23、jsonp的实现原理
 
    首先在客户端注册一个callback, 然后把callback的名字传给服务器。
    此时，服务器先生成 json 数据。
    然后以 javascript 语法的方式，生成一个function , function 名字就是传递上来的参数 jsonp.
    最后将 json 数据直接以入参的方式，放置到 function 中，这样就生成了一段 js 语法的文档，返回给客户端。
    客户端浏览器，解析script标签，并执行返回的 javascript 文档，此时数据作为参数，传入到了客户端预先定义好的 callback 函数里.（动态执行回调函数）
