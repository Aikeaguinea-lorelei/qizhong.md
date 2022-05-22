## call

```js
let person={
    name:frank
    sayHi(){
        //  call里面传什么内容,this就会显示什么内容
        console.log(this.name)
    }
}
person.sayHi.call({name:jack})
  // 输出Jack
person.sayHi.call(person)
  // 输出frank
```


<!-- 例1 -->
```js
function add(x,y){
    return x+y
}
`用call写法`:
add call (undefined,1,2)  // undefined是占this的位,可以替换成任何东西,但是不能没有
`等价于`:
add(1,2)
```


<!-- 例2 -->
```js
let array=[1,2,3]
Array.prototype.forEach2=function(fn){
    for (let i=0;i< this.legth;i++)
        fn(this[i],i)   // this这个时候什么也不是,他被call声明了以后才有意义
}
`call写法`:(指定array是this)  
array.forEach2.call(array,(item)=>console.log(item))
`等价于`:
array.forEach2((item)=>console.log(item))
```



## apply

### this的两种使用方法
1. 隐式传递
   fn(1,2) `等价于` fn.call(undefined,1,2)
   obj.child.fn(1) `等价于` obj.child.fn call(obj.child,1)      
    (指定前面的整体[obj.child]作为this)
2. 显式传递
   fn.call(undefined,1,2)
   fn.apply(undefined,[1,2])



## bind

## 使用bind绑定this:可以让this不被改变
```JS
function f1(p1,p2){
    console.log(this,p1,p2)
}
let f2=f1.bind({name:'frank'})
```
* f2就是f1绑定了this之后的新版本
  f2() 等价于 f1.call({name:'frank'})