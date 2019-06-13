## Ⅰ、函数

**定义：**

封装执行一项专门任务的代码段

**语法：**

```javascript
function 方法名(参数){干啥事}
```

**函数调用**

```javascript
方法名();
```

**参数：**

方法内独有的变量，接受传入数据，再方法内进行处理

参数让方法更灵活，形参指函数定义时的参数，实参指函数调用时传入的参数

**示例：**

```javascript
function grade(grade){
    if(grade >= 90){
    alert("优秀");
    }else if(grade>=60 && grade < 90){
    alert("及格");
    }else{
    alert("不及格");
    }
}

<button onclick="grade(80);">按钮</button>
```

**提升：**

函数提升：函数的定义自动提前到作用域顶部

```javascript
my();
function my(){
    console.log(1);
}
```

变量提升：变量提升是声明提升，赋值不提升

```javascript
console.log(a);
var a = 3;
```

这个会打印undefined

```javascript
my();
var my=function(){console.log(5);}
```

这种会报错：Uncaught TypeError: my is not a function

my只是一个普通的变量

**函数的返回值：**

```javascript
function my(){
    alert(a);
}
var c=my();
console.log(c);
```

结果是undefined，函数没有返回值，运行完之后没有结果

函数需要结果，需要return关键字

return关键字的本意是退出函数运行，如果在return后面有东西，退出函数的同时返回结果

用return返回三个数中的最大值：

```javascript
function getMax(a, b, c){
    var max = a;
    max = a > b ? a : b;
    max = max > c ? max : c;

    return max;
}
```

**作用域：**

作用域表示一个变量的可用范围

全局作用域：全局作用域内声明的变量叫做全局变量

局部作用域：函数内部 局部作用域内声明的变量叫局部变量

```javascript
var a = 3;
function my(){
    a = 6;
}
```

局部(函数)作用域可以使用全局变量，反过来不过可以

函数作用域在函数调用时才创建，函数调用结束之后就销毁

javascript对于未声明的变量会自动全局帮你声明,如下：

```javascript
function my(){
    a = 3;
}
my()；
console.log(a);
```

**闭包：**

函数使用了不属于自己的局部变量，如下：

```javascript
function getCount(){
    var n = 0;
    function getUnique(){
        return n++;
    }
    return GetUnique;
}

var c = getCount();
console.log(c());
console.log(c());
console.log(c());
```

这样写，n定义在函数内部，可以避免全局污染

全局变量容易被篡改，且占内存，建议少用

当然闭包也带来了问题，那就是内存泄露，这里getCount()无法销毁，一直被c挂着，所以也建议少用

## Ⅱ、结构化编程

### 2.1 if判断

if判断作用类似于三目运算符，三目的优势是简便，任何地方可以用，但只能写两个条件，if判断则相反，可以写多个条件，但有的地方用不了

```javascript
if(a > 6){
    alert("a大于6");
}else if (6 == a){
    alert("ad等于6");
}else{
    alert("a小于6");
}
```

if条件中只有6种情况为false，其余都是true

false	0	undefined	null	NaN	""

### 2.2 循环

程序反复执行同一套代码

循环三要素：循环条件、循环变量、循环体

**while**

```javascript
while(条件){循环体;，循环变量的变化;}

var n = 0;
while(n < 5){
    console.log(n);
    n++;
}
```

**for**

```javascript
for(var n = 0; n < 5; n++){
    console.log(n)；
}
```

for用的多，常用作数组遍历
