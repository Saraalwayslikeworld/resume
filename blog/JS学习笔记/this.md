# this

## 1.this的判断

1. this为window的情况
    - 函数被直接调用时this
    ```
    function fn1(){
        console.log(this)   
    }
    fn1()   //输出window
    ```
    - 内部函数的this
    ```
    function fn1(){
        function fn2(){
            console.log(this)
        }
        fn2()
    }
    fn1()  //输出window
    ```
    - setTimeout、setInterval执行函数的this
    ```
    setTimeout(function(){
        console.log(this)
    },1000)
    ```

2. 构造函数内的this指向构造的对象
```
function Person(name){
    this.name = name
}
Person.prototype.sayname = function(){
    console.log(this.name)
}
var p1 = new Person('bill')
p1.sayname()     //输出bill
```
3. 作为对象方法调用时指向对象
```
var obj1={
    name:'bill',
    sayname: function(){
        console.log(this.name)
    }
}
obj1.sayname()
```
4. 绑定事件中this指向事件源DOM对象
```
document.addEventListener('click',function(e){
    console.log(this)  //输出document
    setTimeout(function(){
        console.log(this)  //输出window
    },200)
})
```
---
## 2.改变this指向

1. bind

    **返回一个新函数，使函数内部的this为传入的第一个参数**

    需要注意的是bind返回一个修改后的函数，并不执行它。

    ```
    var obj1={
        name:'bill',
        sayname: function(){
            console.log(this.name)
        }
    }
    var obj2={
        name:'sara'
    }
    obj1.sayname()  //输出bill
    obj1.sayname.bind(obj2)() //输出sara
    ```

2. call和apply
    *调用一个函数，传入函数执行上下文及参数*

    fn.call(context,par1,par2...)

    fn.apply(context,[par1,par2,par3...])
        
        call和apply只有一个区别，就是call()方法接受的是若干个参数的列表，而apply()方法接受的是一个包含多个参数的数组。          ——————MDN
    ```
    function sum(){
        var args = Array.prototype.slice.call(arguments,0)
        console.log(args)
    }
    sum(1,3,2,4)  //输出[1,3,2,4]
    ```
    ```
    var arr=[3,1,0,-3,5]
    console.log(Math.max.apply(null,arr)) 
    ```

3.caller,callee
  
---  
## 3.确定this的技巧

func(p1,p2) 等价于 func.call(undefined,p1,p2)

obj.child.method(p1,p2) 等价于 obj.child.method.call(obj.child,p1,p2)

所有函数调用方式可理解为 func.call(context,p1,p2,...)
因此，

    **this即为call一个函数时传的context，没有传即默认为undefined或null**

    浏览器里有一条规则：如果你传的 context 就 null 或者 undefined，那么 window 对象就是默认的 context（严格模式下默认 context 是 undefined）

用各种例子来验证：
```
    function fn1(){
        console.log(this)   
    }
    fn1()   //fn1.call(undefined) 输出window
```
```
    function fn3(){
        function fn2(){
            console.log(this)
        }
        fn2()  //fn2.call(undedined)
    }
    fn3()   
```
```
var obj1={
    name:'bill',
    sayname: function(){
        console.log(this.name)
    }
}
obj1.sayname() //obj1.sayname.call(obj1)
```
```
function fn1(){
    console.log(this)   
}
function fn2(){
    console.log(this)   
}
var arr=[fn1,fn2]
arr[0]() //arr可看做特殊对象{0:fn1,1:fn2},arr[0]等价于arr['0'],
arr[0]()等价于arr.0.call(arr)
```