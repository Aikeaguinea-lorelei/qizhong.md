## promise用途

### promise对ajax源码的改造
```JavaScript
ajax=(method,url,options)=>{
  // return一个promise函数
  return new Promise((resolve,reject)=>{
    const {success,fail}=options
    const request=new XMLHttpRequest()
    request.open(method,url)
    request.onreadystatechange=()=>{
        if(request.readyState===4){
            // 成功就调用resolve(result),失败就调用reject(error)
            if(reuest.status<400){
                success.call(null,request.response)
            }else if{
                fail.call(null,request,request.status)
            }
        }
    }
    request.send()
  // promise函数一直延伸到这里  
  })
}
```
###  ※所以,要记住这行代码:
```JavaScript
return new Promise((resolve,reject)=>{})
```
* 使用时:用 .then(success,fail) 传入成功函数和失败函数



## Promise.prototype.then() 用法

* then() 方法返回一个 Promise,它最多需要有两个参数：Promise 的成功[fullfillment]和失败[rejection]情况的回调函数。
```JavaScript
const promise1 = new Promise((resolve, reject) => {
  resolve('Success!');
  or
  reject(new Error("出错了！"));
});

promise1.then((value) => {
    console.log(value);    // fulfillment  成功时,返回成功的结果
    // expected output: "Success!"
},reason =>{
    console.error(reason);    // rejection  失败时,返回失败的原因
});
```



##  Promise.all() 用法

* 当promise输入一个数组时,promise all()函数会等数组内的[所有对象都解析完毕]后,`resolve`[最后一个成功的promise对象],或者`reject`[第一个失败的对象]  (无论怎样都只返回一个值)
* 如果返回结果为空,那么最后一个非promise的值仍然会被返回

```JavaScript
// 所有对象都解析成功,且数组中没有promise值.所以结果为一个空对象,所以同步为第3个对象的值
var p = Promise.all([1,2,3]);
// 所有对象都解析成功,所以结果为仅包含第1个promise对象,也就是第4个对象的值
var p2 = Promise.all([1,2,3, Promise.resolve(444)]);
// 第4个对象解析失败,所以结果为第4个对象的reject原因(555)
var p3 = Promise.all([1,2,3, Promise.reject(555)]);

// using setTimeout we can execute code after the stack is empty
setTimeout(function(){
    console.log(p);
    console.log(p2);
    console.log(p3);
});

// logs
// Promise { <state>: "fulfilled", <value>: Array[3] }
// Promise { <state>: "fulfilled", <value>: Array[4] }
// Promise { <state>: "rejected", <reason>: 555 }
```



## Promise.race() 用法

* 一个待定的 Promise 只要给定的迭代中的一个promise解决或拒绝，就采用[第一个promise的值]作为它的值，无论这个promise是成功还是失败. 从而异步地解析或拒绝

```JavaScript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one');
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two');
});

Promise.race([promise1, promise2]).then((value) => {
  console.log(value);
  // 两个都成功,但是promise2更快,因此
});
// 输出two
```