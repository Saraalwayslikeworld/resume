# JavaScript基础
***
1. JavaScript数据类型
    1. 数字（number）：整数和小数
    2. 字符串（string）：字符组成的文本
    3. 布尔值（Boolean）：ture、false
    4. 对象object：各种值组成的集合
    5. undefined：表示未定义
    6. null：表示无值 
    - 原始类型：数字、字符串、布尔值、symbol
    - 复杂类型：对象
    ，分为狭义的对象（object）、数组（array）、函数（function）
***
2. NaN是什么？ 有什么特别之处？     
NaN，not a number，代表任意一个数字。
他的特别在于它属于number数据类型，却没有确定的值，会产生 NaN === NaN为FALSE的结果。
***
3. 立即执行函数表达式      
```
  ( function(){ statement } )()
  ( function(){ statement }() )
```
立即执行函数表达式是声明一个匿名函数，马上执行这个匿名函数。
它的作用是创建独立的作用域，内部变量无法被外部访问。
***
4. 数组方法     
```
var arr = [ 3,6,9,1,-1] 
arr.push( 'hello' )    //  push 在数组末尾增加一个元素
console.log(arr)     //  [ 3,6,9,1,-1,'hello' ] 
var a = arr.pop       //  pop将数组最后一个元素拿出
console.log(a)        //  'hello'
console.log(arr)      // [ 3,6,9,1,-1 ]
a = arr.shift            // shift去除数组第一个元素
console.log(a)       // 3
console.log(arr)     // [ 6,9,1,-1 ]
arr.unshift('world')  // unshift在数组的第一位新增元素
console.log(arr)     //  [ 'world',6,9,1,-1 ]
var arr2 = arr.splice(2,3)  // arr.splice(开始元素下标，删除元素个数，新增元素）
console.log(arr2)   // [ 9,1,-1 ]
console.log(arr)     // [ 'world',6 ]
arr.splice(1,0,8,9,11)
console.log(arr)     // [ 'world',8,9,11,6 ]
var str = arr.join('-')// join将数组转化为以（）内字符连接的字符串
console.log(str)     // "world-8-9-11-6"
console.log(arr.reverse())//[6, 11, 9, 8, "world"] ,reverse实现数组倒序
arr.sort(function(a,b){
    return a - b;
})                           // sort 通过函数实现排序 [6, 8, 9, 11, "world"]
var arr3 = [ 5,10 ]
console.log(arr.concat(arr3))//concat 将两个数组连接形成一个新数组 [6, 8, 9, 11, "world",5,10 ]
```
***
5. ES5数组方法 indexOf、forEach、map、every、some、filter、reduce       
- .indexOf(element) 查找制定元素位置
```
var arr = [ 1,2,5,8,-1,0,10,'hello' ]
arr.indexOf(0)  //返回指定元素的位置5
arr.indexOf(3)  // 没有则返回-1
```
- .forEach(function(element, index, array){})  遍历数组
```
var arr = [ 1,2,5,8,-1,0,10,'hello' ]
arr.forEach(function(e,i,arr){
    arr[i] = e * e;
})                          // 原数组改变，返回原数组[1, 4, 25, 64, 1, 0, 100, NaN]
```
- .map(function(element)) 遍历数组，返回新数组，数据结构同原数组。
```
var arr = [ 1,2,5,8,-1,0,10,'hello' ]
arr.map(function(e){
    return e + 1;
})                         // [2, 3, 6, 9, 0, 1, 11, "hello1"]
```
- .every(function(element,index,array){})遍历数组进行逻辑判断
函数的每个回调函数都返回true的时候才会返回true，当遇到false的时候终止执行，返回false
```
var arr = [ 1,2,5,8,-1,0,10,'hello' ]
arr.every(function(e,i,arr){typeof e == 'number'}) //false
```
- some(function(element,index,array){})遍历数组进行逻辑判断
“存在”有一个回调函数返回true的时候终止执行并返回true，否则返回false
```
var arr = [ 1,2,5,8,-1,0,10,'hello' ]
arr.some(function(e,i,arr){typeof e == 'number'}) //true
```
- .filter(function(element){})回调函数逻辑判断，为true则元素加入返回数组，为false则不加入。
```
var arr = [ 1,2,5,8,-1,0,10,'hello' ]
arr.filter(function(e){ return (typeof e) == "number"}) //[1, 2, 5, 8, -1, 0, 10]
```
- .reduce(function(v1,v2){ },value)遍历数组，将数组元素组合成一个值
```
var arr = [ 1,2,5,8,-1,0,10,'hello' ]
arr.reduce(function(v1,v2){ return v1+v2 },0) //"25hello"
```
***
6. 正则表达式
```
\d                    数字字符
\w                   字母数字字符，还包括下划线
\s                    空白字符
[a-zA-Z0-9]     字母数字字符
\b                    单词边界，指[a-zA-Z_0-9]之外的字符
.                      除换行字符和回车符以外的任意字符
*                      出现次数无限次
+                     出现次数>=1次
？                    出现<=1次，量词后的？表示非贪婪模式
x{3}                 x出现3次
^                     匹配输入开始，在[ ]内表示取反
$                     匹配输入结尾      
```   
***
7. 简单解释单线程、任务队列的概念。
- 单线程：JS执行代码时只在一个线程上运行，也就是说同时只能执行一个任务，其他任务排队等候。所有的同步任务是放在单线程内的。
- 任务队列：任务队列内是异步任务，当所有单线程内的同步任务执行结束后，会判断任务队列里的异步任务是否满足执行条件，满足就会将其放到主线程内作为同步任务执行。可以认为单线程是预约挂号，病人按预约挂号的顺序优先看病，而任务队列是普通病人，等预约病人看完了才能挂号看病。
***
8. DOM2事件传播机制     
DOM2事件传播分为3个阶段：
事件捕获阶段，
处于目标阶段，
事件冒泡阶段。
首先发生的是事件捕获，为截取事件提供机会，然后实际目标接受事件，最后事件冒泡。
![](http://p5s9qkvol.bkt.clouddn.com/18-4-11/35052285.jpg)
***
9. onlick与addEventListener的区别？     
|onclick|addEventListener|
| ---- | :---: | ----: | 
|一个对象同类事件只能绑定一个，否则会被新的事件覆盖|一个对象多次绑定同一类事件|
|只能在冒泡阶段绑定事件|可以在冒泡或捕获阶段绑定事件|
|只对HTML元素有效|可以选择任何DOM元素|  

***
10. JS原生DOM       
```
document.getElementById()                //id选取元素
document.getElementsByClassName()        //类名选取元素
document.getElementsByTagName()          //标签选取元素
document.getElementsByName()             //name属性选取元素
document.querySelector()                 //选取符合的第一个元素
document.querySelectorAll()              //选取所有符合的元素
```
```
document.createElement('node')                   // 创建元素节点
document.createTextNode('content')               // 创建文本节点
document.createDocumentFragment()                // 创建DOM片段
node.appendChild(newElement)                     // 在元素末尾添加元素
node.insertBefore(newElement, orgElement)        // 在某元素前添加元素
node.replaceChild(newElement,oldElement)         // 新元素取代某个元素
```
***
10. 事件传播机制、阻止传播、取消默认事件、事件代理

- 事件传播机制：
 1. 事件捕获：事件从DOM树的根节点一直向下传播到目标元素。
 2. 事件冒泡：事件从目标元素逐级向上传播，直至根节点。
 3. DOM2事件流：包括三个阶段，事件捕获阶段，处于目标阶段，事件冒泡阶段，首先发生的是事件捕获，为截取事件提供机会，然后是实际目标接收事件，最后是冒泡阶段。
- 阻止传播：在支持addEventListener()的浏览器中，可以调用事件对象的stopPropagation()方法以阻止事件的继续传播。如果在同一对象上定义了其他处理程序，剩下的处理程序将依旧被调用，但调用stopPropagation()之后任何其他对象上的事件处理程序将不会被调用。
- 取消默认事件：在支持addEventListener()的浏览器中，可以通过调用事件对象的preventDefault()方法取消事件的默认操作。
- 事件代理：利用了浏览器的事件冒泡和事件源（target）。在js中事件会冒泡到父级节点，可以在父级节点进行事件代理，事件的目标元素在父元素对象中以属性的形式出现。
演示demo
https://github.com/Saraalwayslikeworld/resume/blob/master/projects/%E4%BA%8B%E4%BB%B6%E4%BC%A0%E6%92%ADdemo.html
![阻止传播](http://sara-demo.oss-cn-beijing.aliyuncs.com/18-3-3/49085358.jpg)
![事件传播](http://sara-demo.oss-cn-beijing.aliyuncs.com/18-3-3/62333732.jpg)
***
11. window.onload 和 document.onDOMContentLoaded 

* window.onload :页面所有资源加载完毕。
* document.onDOMContentLoaded:DOM结构解析完毕。
```
//当页面所有资源加载完毕后获取图片宽高
var img = document.querySelector('img')
img.onload = function(){
    console.log(img.width)
    console.log(img.height)
}
```
```
//当DOM结构解析完毕后可获取元素宽高
var em = document.querySelector('div')
em.onDOMContentLoaded= function(){
    console.log(em.offsetWidth)
    console.log(em.offsetHeight)
}
```
***
12. cookie & session &localStorage 

- cookie
 cookie是浏览器访问某服务器后，服务器返回的一小段数据。浏览器每次访问该服务器都必须带上这段数据，因此cookie大小有限制4K。cookie往往有时效。
- session
 session是存储在服务器内存或数据库中的一小段数据，用户将数据提交到服务器后服务器创建session用于记录用户的相关信息。 session创建后会将对应的session_id作为cookie种到浏览器上。**session是实现服务器识别用户的一种手段，其中应用了cookie。**
- localStorage
localStorage是浏览器本地存储的端口，可以将最大5M的数据保存在浏览器中，永不过期失效，除非JS手动清除。它常被用于存储图片、js等等，不参与网络传输。
***
