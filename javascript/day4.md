## Ⅰ、引用数据类型

引用数据类型保存在堆中，栈中保存起对应的地址(指针)

### 1.1 数组

数组是连续存储多个数据的存储空间

**创建：**

```javascript
字面量形式：
var arr = [1, 2, 2];
构造函数形式：
var arr = new Array(1, 2, 3);
```

arr在栈中保存一个指针指向队中的数据，所以叫引用数据类型

数组有索引，默认从0开始，通过索引访问到数组中的值

数组有length，表示数组有多少个元素

```javascript
console.log(arr[0]);
console.log(arr.length);
```

**引用体现：**

```javascript
var arr = [1, 2, 3, 4, 5];
var b = arr;
b[0] = 9;
console.log(arr);
```

arr的地址给了b，b也指向了原来的数据，所以数据被篡改成功了，即指针被复制了一份

**垃圾回收：**

垃圾回收机制：js会自动销毁不再被引用的对象

堆里面存放的都是对象，null用来主动释放对象，是一个空对象指针，属于object

```javascript
arr = null;
切断栈和堆的联系
```

**数组遍历：**

```javascript
var week = ["日", "一", "二", "三", "四", "五", "六"];
    for(i = 0, i < week.length, i++){
        week[i] = "星期" + week[0];
    }
    console.log(week);
```

### 1.2 对象

对象是多个键值对的集合，属性名: 属性值

属性名必须是字符串且不得重复，如果不是字符串也会被强制转成字符串，属性值可以为任意数据类型

**创建：**

```javascript
字面量形式：
var arr={
    "name": "小明",
    "age": "18",
    "my": function(){alert("2333");}
};
console.log(arr.name);
arr.name="小红";
console.log(arr.name);
arr.my();

构造函数形式：
var person = new Object();
person.name = "";
```

方法也可以作为对象的属性，方法名作为属性名，方法体作为属性值

对象的属性名如果是变量，不能用点访问

```javascript
var name = 'ahh';
var person = {[name]: "小明"};
console.log(person[name]);
```

**对象遍历**

```javascript
for(var key in person){
    console.log(key);
    console.log(person[key]);
}
```



## Ⅱ、内置对象

刚才上面写的是我们自己创建的对象，叫自定义对象，现在整理一下javascript的内置对象和给我们准备好的属性和方法

### 2.1 关于字符串

```javascript
toUpperCase()字母转大写
toLowerCase()字母转小写
indexOf()查找关键字 默认只能找到第一个关键字位置 找不到返回-1
substring(i,j)截取子字符串,含头不含尾，只给i，表示从i截到最后
slice()同上，原本用于数组，但在字符串中也能用
split('x')字符串切割成数组,根据x连
concat()连接多个字符串，数组中也能用,字符串中用加号也可以
toString()转成字符串

var str  = "hello";
str.toUpperCase();

补充：
window是内置对象，window可以省略
window.paresInt()
paresInt() 取字符串中整数开头的部分
parseFloat() 取字符串中小数开头的部分
var a = 12.56；
a.toFixed(N) 按N位四舍五入取整

```

### 2.2 关于数组

```
slice()
join('x')数组合成字符串 x为连接符
concat()连接多个数组
以上三个和字符串相关的 不能直接修改数组，需要新创建变量来接受处理后的结果

push()给数组结尾追加元素
pop()移除数组最后一个元素
unshift()在数组开头追加元素
shift()移除数组开头元素
reverse()反转数组
sort()按unicode排序
sort(function(a,b){return a-b})给数组元素排序，根据unicode编码排序，注意
里面加一个function就可以正常排序了

splice()删除，插入，替换数组中指定元素
arr.splice(i,j,a,b,c)从i个开始删j个,a,b,c为插入的新值，直接插入的话j为0

```

### 2.3 正则

RegExp，专门验证字符串中字符出现的规律

/开头/结尾

```javascript
[]用来放备选字符，一个中括号只能代表一位字符的匹配规则
[]中如果只有一位备选字符或者只有一个预定义字符则中括号可以省略
正则表达式对于任何连续的区间都可以用横线连接

数量词{}用来表示前一位规则重复多少次，如果想修饰多位，加小括号
{num} {min,} {min,max}
       
特殊数量词 ? * +
?代表前面一位规则可有可无，最多一次 等价于{0,1}
*代表前面一位规则可有可无，不限制次数
+代表前一位规则至少出现一次
       
预定义字符集
对于正则表达式中有特殊含义的字符需用反斜杠转移
\d代表所有数字
\w代表所有数字字母下划线
\s代表空格
.代表任意字符
       
test 用来验证字符串格式是否正确，正确返回true，错误返回false
语法：reg.test("被检验数据");
test方法，默认是部分匹配
            
解决方案：
在整条正则表达式加^表示以...开头，在整条正则表达式加$代表以...结尾

```

**案例：**

```javascript
手机号码：
var reg = /^1[3-9]\d{9}$/；
var num = '18667915923'；
if(reg.test(num)){
    alert("注册成功")；
}else{
    alert("输入格式有误")；
}

邮箱：
reg = /^\w+@\w+([-]\w+)*(\.\w+)+$/；

构造函数形式创建正则表达式：
var regexp = new RegExp();
```

### 2.4 Math

Math: 封装了所有与数学计算相关的api

Math对象不需要创建，直接使用即可

```javascript
Math.ceil() 向上取整
Math.floor() 向下取整
Math.min()/max() 取最值  不能放数组
传数组的话 在es6中 给数组名前加...：Math.max(...arr)
Math.random() 取[0,1)随机数
取任意min-max之间的随机数：Math.random()*(max - min + 1) + min
Math.abs() 取绝对值
```

### 2.5 Date

封装了一个时间点数据,提供了对日期操作的api

```javascript
new Date()默认返回当前时间
toLocalTimeString 转为当地时间的字符串
var date = new Date().toLocalTimeString;

日期之间可以直接坐差值，间隔毫秒数
var date = new Date("2019-11-11 00:00:00")
var now = new Date();
console.log(date - now)

getDate() 获取日
getFullYear()
getMonth() 返回0到11 +1修正
getDay() 返回0到6 0是周日
getHours() 0-23
getMinutes() 0-59
getSeconds() 0-59
getTime() 1970-01-01至今的毫秒数
以上所有方法get改为set就是设置某个时间，getDay()除外
setMonth() 要减1修正

```



## Ⅲ、小练习

### 3.1 数组去重

```javascript
function unique(arr){
    var hash = [];
    for(var i = 0; i < arr.length; i++){
        if(-1 == hash.indexOf[i]){
            hash.push(arr[i]);
        }
    }
    
    return hash;
}

```

### 3.2 字符串中单词首字母大写

```javascript
function First_Word_Upper{
    var arr_words = str.split(" ");
    for(var i = 0; i < arr_words.length; i++){
    arr_words[i] = arr_words[i][0].toUpperCase + arr_words.substring(1);
    }
    return words.join(" ");
}

```

### 3.3 四位随机验证码，包含英文大小写和数字

```javascript
//unicode编码 数字：48-57 大写字母 65-90 小写字母 97-122
String.fromCharCode() unicode转为对应字符
function confirm(){
    var codes = [];
    for(var i = 48; i <= 57; i++){
        codes.push(i);
    }

    for(var i = 65; i <= 90; i++){
        codes.push(i);
    }

    for(var i = 97; i <= 122; i++){
        codes.push(i);
    }

    var arr = [];
    for(var i = 0; i < 4; i++){
        var index = Math.floor(Math.random()*(codes.length + 1 - 0) + 0);
        var char = String.fromCharCode(codes[index]);
        arr.push(char);
    }

    return arr;
}
```
