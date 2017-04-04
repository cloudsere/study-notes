### js实现继承的方法

#### 使用构造函数

```javascript
function Person(name){
  this.name = name;
  this.say = say;
}
function say(){
  console.log('I am ' + this.name);
}
var lesley = new Person('lesley');
lesley instanceof Person //true
Person.prototype //Object{}
lesley.prototype //undefined
lesley.constructor //function Person(){}
```

在用```new```调用构造函数时

1. 创建一个空对象并且this变量引用了该对象，同时还继承了该函数的原型
2. 属性和方法被加入到this引用的对象中
3. 最后隐式地返回this

但上面的做法会为每个Person的实例都创建一个新的函数，很低效，所以应该将方法添加到Person的原型中

```javascript
//可重用的成员应该添加到原型中
Person.prototype.say = function(){
  console.log('I am ' + this.name);
};
```



### 函数声明和变量声明同名怎么办？

> 1. 函数声明会置顶
> 2. 变量声明也会置顶
> 3. 函数声明比变量声明更置顶
> 4. 变量和赋值语句一起书写，在js引擎解析时，会将其拆成声明和赋值2部分，声明置顶，赋值保留在原来位置
> 5. 声明过的变量不会重复声明

比如

``` javascript
var a = 3;
function a(){
	console.log('lesley');
}
typeof a;//number
```

上面这段代码其实等于：

```javascript
var a;
function a(){
	console.log('lesley');
}
a = 3;
typeof a;
```

