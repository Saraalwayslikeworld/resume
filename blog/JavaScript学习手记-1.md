# 关于 if(xx)与 a == b 的判断

## if(xx)的判断
####1.if(number)
  **当 if(number)，0、NaN为false,其他值为true**
```
var a = 5
if(a){
    console.log('true')
} // true
a = 1
if(a){
    console.log('true')
} // true
a = 0
if(a){
    console.log('true')
} // false
a = -1
if(a){
    console.log('true')
} //false
a = NaN
if(a){
    console.log('true')
} //false
```

####2.if(string)
  **当 if(string)，空字符串为false,其他为true**

```
if('hello'){
    console.log('true')
} // true
if('   '){
    console.log('true')
} // true
if(''){
    console.log('true')
} // false
if('0.00'){
    console.log('true')
}
```

####3.if(boolean)
  **当 if(boolean)，直接判断**

```
if(true){
    console.log('true')
} // true
if(false){
    console.log('true')
} // false
```

####4.if(object)
  **当 if(object)，为true**

```
if([1,3,4]){
    console.log('true')
} // true
function f(){
   var b = 1 + 2;
   return b; 
}
if(f()){
    console.log('true')
} //true
```

####5.if(undefined)
  **当 if(undefined)，为false**

```
if(undefined){
    console.log('true')
} //false
```

####6.if(null)
**当 if(null)，为false**

```
if(null){
    console.log('true')
} //false
```

## a == b 的判断
对于相同类型的a、b，相等的判断较简单。以下主要讨论不同数据类型的a、b之间进行相等运算时的判断。

####1. string == number
  **结果为 toNumber(a) == b ，当a无法转换为number时判断相等为false**

```
 "" == 0           //true
 "  " == 0         //true
 "hello" == 0      //false
 "hello" == 1      //false
 "2" == 2          //true
```

####2. boolean == (any)
  **Boolean在相等运算时会转换为数值，true为1，false为0。**

```
 "" == true           //false
 "" == false          //true
 " " == true          //false
 "hello" == true      //false
 1 == true            //true
 0 == false           //true
 undefined == false   //false
 undefined == true    //false
 null == false        //false
 null == true         //false
```

####3. object == number/string
  **object会试图使用valueOf和toString转换后比较**

```
var obj = { 
  a: 0, 
  valueOf: function(){return 1} 
} 
obj == 1   //true
[] == 0    //true
[2] == 2   //true
```

####4. null == undefined //true

## toNumber
   
undefined  -->  NaN 
null            -->  0 
boolean     -->  true:1, false:0 
string         --> "abc":NaN,"123":123
   
##总结：
  **做相等运算时，一般倾向于将不同的数据类型都转化为数值，或是转化为相同的数据类型.**
- 如果两个值类型相同，则执行严格相等的运算
- 如果两个值的类型不同
   1. 如果一个是null，一个是undefined，那么相等
   2. 如果一个是数字，一个是字符串，先将字符串转为数字，然后比较
   3. 如果一个值是true/false则将其转为1/0比较
   4. 如果一个值是对象，一个是数字或字符串，则尝试使用valueOf和toString转换后比较
   5. 其它就不相等了 