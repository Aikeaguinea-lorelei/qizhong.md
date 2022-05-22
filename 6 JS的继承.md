## 基于原型的继承

1. `共有属性的集合`就是[原型]
2. [原型中的内存] 存着`共有属性` 

### 如何确定一个对象的原型:

let a=new A() 的原型是A.prototype

* 你是谁构造的,你的原型就是谁的prototype属性对应的对象
  **公式:对象.__Proto__===它的构造函数.prototype**

  如上例,a由A构造,则a的原型(__Proto__)和A.prototype共用一个属性(#309)

  A.prototype:#309
  对应
  a.__Proto__:#309

* 区别:prototype来自于windows上面的object  
     而__Proto__来自于声明的空数组a
    (Object.prototype是本来就存在的.没有原型,不存在由哪个函数构造成)

[用原型的方法构造一个圆]:
```JS
founction Circle(radius)={
    this.Radius=radius
}
Circle.prototype.getArea=function(){
    return Math.PI * this.Radius * this.Radius
}
Circle.prototype.getLength=function(){
    return  2 * Math.PI * this.Radius
}

let circle=new Circle(3)
// 输出:circle.Radius=3
//     circle.getArea=
//     circle.getLength=
```



## 基于class的继承

[用class的方法重新构造圆]:
```JS
class Circle{
    constructor(radius){
        this.radius=radius
    }
    getArea(){
        return Math.pow(this.radius,2) * Math.PI
    }
    getLength(){
        return this radius * 2 * Math.PI
    }
}
let circle=new Circle(3)
circle.radius
circle.getArea()
circle.getLength()
```