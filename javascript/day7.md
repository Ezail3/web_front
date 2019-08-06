## Ⅰ、Navigator

浏览器对象

判断浏览器版本

```javascript
<script>
	console.log(navigator.userAgent)
	//userAgent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36
	//userAgent:保存浏览器名称和版本号
	var str = navigator.userAgent;
	if(str.indexOf(-1 != "Chrome")){
	alert("谷歌浏览器");
	}else{

	}
</script>
```



## Ⅱ、原型和继承

prototype：方法背后专门保存由方法创建出来的对象共有的数据

### 2.1 构造函数

对象模板——专门用来反复创建相同结构的对象的方法

```javascript
//首字母大写
function Student(name,age,height){
    this.name = name;
    this.age = age;
    this[height] = height;
    //属性名是变量要用[],值可以直接是变量不用[]
}

var ll = new Student("李雷",18,170);
var hmm = new Student("韩梅梅",17,165);
```

### 2.2 私有属性与共有属性

```javascript
ll.car = "bma";
//car是私有属性，属于ll这个实例对象自身的
Student.prototype.car = "bma";
Student.prototype.my = function(){
    console.log("我会泡妞");
}
//共有属性：由同一构造函数创建出来的对象共同享有的属性
//对象有原型吗？不一定，方法这个对象有原型，其他的对象没有原型，方法是一个特殊的对象，prototype是他的属性，它的值指向一个原型对象(多个公有属性)
<div style="widy: 200px;height:200px"></div>
//style是个样式属性，它的值指向一个样式对象(key:value)
console.log(hmm);
//会发现car不是hmm的属性
console.log(hmm.car);
//但是开一下她爹的car还是可以的
ll.car = "benz";
//这个car是ll的私有属性，自己买的benz，私有属性
```

任何实例对象，没有权利修改原型中的数据，如果子类实例给原型中的属性重新赋值，其实是创建一个同名的私有属性，只有构造函数有权利修改原型中的数据

### 2.3 继承

使用现有类型，创建出新的类型，新的类型中可以使用现有类型的属性和方法，也可以拓展出现有类型没有的属性和方法



## Ⅲ、原型链

- js中方法也是对象，对象都是由构造函数创造的
- Function是所有function的父类型(女娲)
- Object是所有对象的父类，是Function的子类，因为他是一个构造函数，是函数
- __proto__隐式原型    对象有隐式原型，用来实现继承，一个对象的隐式原型永远指向创建这个对象的构造函数的原型对象

原型链就是一条继承链



## Ⅳ、new关键字

new做了什么？

1、创建一个空对象	var ll = {};

2、将ll的隐式原型指向原型对象

3、改变this指向(call apply)，加属性

4、返回一个全新的对象
