# ES6-2-箭头函数+参数处理

## 1.箭头函数

    ```
    let arr = [1,3,4,2,0]
    arr.map(e=>e+1)
    ```
箭头函数最大的好处---避免了this的混淆。

这里不可避免再回顾一下this，一句话：

**this即为call一个函数时传的context，没有传即默认为undefined或null（即为window）**

***
## 2.函数默认参数

首先来个基础版
```
function sum(x=0,y=1){
    return x+y
}
sum()  // 1
sum(1) // 2
sum(1,2) // 3
```
很简单，升个级？
```
function sum([x=0,y=1]){
    return x+y
}
sum()    //啊哦报错了，注意与上个例子的区别，这里可以看做对参数的属性设置默认值，而不是对参数本身设置默认值，不给形参不行的
sum([])  // 1
sum([1]) // 2  少给了，默认值补上
sum([1,2]) // 3
sum([1,2,3]) //3 多给的直接忽略了
```
修复上个例子不给参数报错的BUG
```
function sum([x=0,y=1]=[0,1]){
    return x+y
}
sum()    // 1 没给参数，默认值补上
sum([])  // 1
sum([1]) // 2  
sum([1,2]) // 3
sum([1,2,3]) //3 
```
## 3.剩余参数

    function(a,b,...c){} // c即为剩余参数。

    如何将arguments转化为真数组？
    ```
    方法1
    let args = [...arguments] //...xxx就是取到剩余参数的方法
    方法2 
    let args = Array.from(arguments) //Array.from()是ES6新增的转化数组的API
    方法3
    let args = Array.prototype.slice.call(arguments) //es5调用数组方法
    ```
## 4.展开操作

    简单的语法糖，所见即所得。

    let arr1 = [1,3,9,2]
    let arr2 = [0,...arr1,5] = [0,1,3,9,2,5]
    let [,,...arr3] = arr1 //arr3 = [9,2],注意这样操作时arr3必须是最后一个元素,否则报错