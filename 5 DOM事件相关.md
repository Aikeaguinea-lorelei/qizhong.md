## 什么是事件委托

* 事件委托,就是把一个元素[响应事件的函数]委托到另一个元素,一般把事件委托到`目标函数A`的[父元素B],或者是[更外层的元素]
当设置了一个事件需要函数A响应时,会`通过冒泡`触发[父元素B]响应

[作用]: 
1. 要给很多个按钮添加点击事件:
   可以监听他们的祖先元素,冒泡的时候再判断target是不是其中之一
2. 要监听目前不存在的元素的点击事件:
   可以监听祖先元素,等点击的时候再查看是不是想要监听的那个元素

[举例]:
```HTML
<script src="监听.js"></script>
    <div id="div1">

    </div>
    <div id="div2">
        <button>click 1</button>
        <button>click 2</button>
        <button>click 3</button>
        <button>click 4</button>
        <button>click 5</button>
        <button>click 6</button>
        <button>click 7</button>
        <button>click 8</button>
        <button>click 9</button>
        <button>click 10</button>
    </div>
```
```JavaScript
// 在div内创建一个按钮,一秒钟后浮现
setTimeout(()=>{
    const button=document.createElement('button')
    button.textContent='click 1'
    div1.appendChild(button)
},1000)

// 监听div1
div1.addEventListener('click',(e)=>{
    const t=e.target
    if(t.tagName.toLowerCase()==='button'){
        console.log('button被click,内容是'+t.textContent)
    }
})
```



## 怎么阻止默认动作

有一些事件是不支持取消冒泡的,比如scroll.所以阻止scroll这个默认事件没用.
那么要阻止页面滚动,就需要在委托函数里用`preventDefault()`阻止[滚轮]或者[触屏滚动]事件
```JavaScript
//  禁用默认事件:滚轮
x.addEventListener{'wheel',(e)=>{
    e.preventDefault()
}}
//  手机中禁用默认事件:触屏滚动
x.addEventListener{'touchstart',(e)=>{
    e.preventDefault()
}}
```
    (注意:需要找准[滚动条所在的]元素)
    (此时滚动条还可以用,所以需要在css里让滚动条width为0)



## 怎么阻止冒泡

假设html中有一堆代码
```html
<div class="1">
    <div class="2">
        <button class="butt">catch me</button>
    </div>
</div>
```
当button事件被触发时,作为父代元素的[2]和[1]会被依次触发.
如果不想让这两者触发的话,就需要用到阻止冒泡
* 方法:在需要组织冒泡的代码后添加`return false`或者`event.stopPropagation()`
```JavaScript
$('.butt').on('click',function(){
    return false  // 或者event.stopPropagation()
})