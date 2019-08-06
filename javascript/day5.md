## Ⅰ、异常处理

异常处理常用于日常代码调试

## 1.1 异常类型

```javascript
所有错误的父类型——Error:
6种子类型
SyntaxError       语法错误
ReferenceError    指向错误
TypeError         错误地使用了类型和类型的方法
EvalError         非法调用eval()
RangeError        参数超出范围
URIError          错误调用全局URI处理函数
```

### 1.2 异常处理语法

```javascript
try
{
	可能出错的代码;
}
catche(err){
	错误处理代码;
}
finally{
	出不出错都执行;（不常用）;
}
```



## Ⅱ、DOM操作

DOM全称document object model

DOM操作通俗点讲就是对网页上的元素进行增删改查

### 2.1 查

**根据id查**

```javascript
var box_id = document.getElementById("box");
//返回一个元素对象
```

**根据class查**

```javascript
var box_name = document.getElementsByClassName("box");
//返回一个数组
consolse.log(box_name[0]);
```

**根据标签查**

```javascript
<div id="sbox">
    <ul>
    	<li>1</li>
		<li>2</li>
		<li>3</li>

    </ul>
</div>
var sbox = document.getElementById("sbox");
var li_arr = sbox.getElementsByTagName("li");
console.log(li_arr);
//返回一个数组
```

**根据name查表单元素**

```javascript
document.getElementByName("xxx");
```

**根据css选择器查找**

```javascript
document.querySelector("#sbox li")
//#sbox表示id为box，.box表示class为box
//返回元素对象，找到第一个就不找了
document.querySelectorAll()
//返回数组，查找所有满足条件的
```

### 2.2 改

**innerHTML**

元素开始标签到结束标签之间的内容(不局限于文字)

```javascript
var box = document.getElementById("box");
console.log(box.innerHTML);
box.innerHTML = "<h1>hello world!!!<h1>";
```

**innerText**

元素开始标签到结束标签之间的文本内容

```javascript
box.innerHTML = "hello world!!!";

```

innerText就按文字识别，innerHTML可以识别html结构，innerText能干的innerHTML都能干

**修改元素属性**

- 通过元素对象的形式修改开始标签里的内容

  没有就加，写在标签外面的内容管不着

```javascript
.box{width: 200px;height: 200px; background: red}

<div class="box" id="box"></div>

var box = document.getElementById("box");
box.id = 'xxx';
box.src = 'xxx';
...
console.log(box.style.width);
//拿到是空，证明dom修改元素css样式其实操作的是内联样式
box.style.width = "300px";
//下面这个要注意，es6中提出class概念，所以这里需要区别对待，这里的className是指class
box.className = 'xxx';

```

- 设置属性传属性名和属性值(用的不多)

```javascript
box.setAttribute("属性名","属性值");
box.getAttribute("属性名");

```

**有个问题**

innerHTML里不支持的html结构换行(引号换行后无法被识别为一对)

**解决：**

- 方法1：

  es5中把html结构的每一行做成一个字符串，用加号拼接起来

- 方法2：

  es6中把引号用`替换掉，这叫模板字符串，支持换行

**反引号功能扩展**

```javascript
字符串中传参数
var name = "小明";
老办法：
"<h1>" + name + "<h1>"
es6：
`<h1> ${name} <h1>`

```

### 2.3 删

**删内容**

```javascript
box.innerHTML = "";

```

**删属性**

```javascript
box.removeAttribute("xxx");
//直接置空的话属性还在，box.id = ""

```

**删自己**

必须通过父级来删除

```javascript
爹元素对象.removeChild(子元素对象);

```

### 2.4 增

**加元素**

```javascript
var ele = document.createElement("h1");
ele.innerHTML = "我是js创造的元素";
爹元素对象.appendChild(子元素对象)；
//向父元素对象最后追加
//创建==》加内容==》追加到爹下面(2，3两步顺序无所谓)

```



## Ⅲ、DOM事件

### 3.1 点击事件

```javascript
<body>
    <button id="btn" onclick="my()">按钮</button>
    <script>
        function my(){
            alert(1);
        }
    </script>
</body>

```

onclick写在开始标签里面，那我们就可以通过对象操作，如下：

```javascript
<body>
    <button id="btn">按钮</button>
    <script>
        var btn = document.getElementById("btn");
        function my(){
            alert(1);
        }
        btn.onclick = my;
	    //注意这里my不带括号，上面属性值在html中是一个字符串，这里需要的是方法的内容，加小括号是让方法执行了
		//这种写法并没有在开始标签中加onclick属性，removeAttribute删除不掉这个属性
		//btn.setAttribute("onclick","my()");		这样也可以绑定事件，但不常用
    </script>
</body>

```

**匿名函数写法**

```javascript
<body>
    <button id="btn">按钮</button>
    <script>
        var btn = document.getElementById("btn");
        btn.onclick = function(){
            alert(1);
        }
    </script>
</body>

```

### 3.2 鼠标划过事件

```javascript
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .box{width: 200px; height: 200px; background: red}
    </style>
</head>
<body>
    <button id="btn">按钮</button>
    <div class="box"></div>
    <script>
        var btn = document.getElementById("btn");
        var box = document.getElementsByClassName("box")[0];
        btn.onclick = function(){
            box.style.background = "blue";
        }
        box.onmouseover = function(){
            console.log("我来了！");
        }
        box.onmouseout = function(){
            console.log("我走了！");
        }
        box.onmousemove = function(){
            console.log("我动了！");
        }
    </script>
</body>

//下面常用于输入框
//onfocus 获得焦点
//onblur 失去焦点

```



## Ⅳ、作业

### 4.1  用户登陆需求：

​	用户名4到8位数字字母组合	输入不对，红色提示不正确，正确，红色消失

​	密码	6位数字

​	按钮	点击只判断有没有填，没填alert xxx不能为空，两个都没填 alert请填写信息

```javascript
<body>
    <div style="width: 200px;margin: auto">
        <form style="width: 200px">
            <input id="uname_input" type="text" placeholder="用户名" name="user_name" value=""><br>
            <span id="uname_err" style="color: white">invalid user name</span><br>
            <input id="pwd_input" type="password" placeholder="密码" name="password" value=""><br>
            <span id="pwd_err" style="color: white">invalid password</span><br>
            <input id="login_btn" type="button" value="登陆">
        </form>
    </div>

    <script>
        var uname_input = document.getElementById("uname_input");
        var uname_err = document.getElementById("uname_err");
        var pwd_input = document.getElementById("pwd_input");
        var pwd_err = document.getElementById("pwd_err");
        var reg = document.getElementById("reg");
        var user_model = /^\w{4,8}$/;
        var pwd_model = /^\d{6}$/;

        uname_input.onfocus = function(){

            uname_err.style.color = "white";
        }

        uname_input.onblur = function(){
            if(!user_model.test(uname_input.value)){
                uname_err.style.color = "red";
            }
        }

        pwd_input.onfocus = function(){

            pwd_err.style.color = "white";
        }

        pwd_input.onblur = function(){
            if(!pwd_model.test(pwd_input.value)){
                pwd_err.style.color = "red";
            }
        }

        login_btn.onclick = function(){
            if(""===uname_input.value && ""===pwd_input.value){
                alert("pls input ur information");
            }else if(""===uname_input.value){
                alert("user name is empty");
            }else if(""===pwd_input.value){
                alert("password is empty")
            }
        }
    </script>
</body>
```

### 4.2 选项卡

鼠标划过选项卡，选项卡变绿，点击选中则下方大框框中文字切换为对应选项卡的名字

```javascript
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }

        .nav{
            width: 1200px;
            height: 40px;
            margin: auto;
            background-color: #999999;
        }
        .nav li {
            list-style-type: none;
            cursor: pointer;
            width: 240px;
            line-height: 40px;
            color: #ffffff;
            text-align: center;
            float: left;
        }
        .nav li:hover{background: darkgreen}

        .content{
            width: 1200px;
            height: 500px;
            background-color: darkgreen;
            margin: auto;
        }

        .chose{
            display: block;
            margin: auto;
            text-align: center;
            line-height: 500px;
            color: white;
        }
    </style>
</head>
<body>
<ul class="nav">
    <li id="tab1" onclick="chose_card(`tab1`)">Tab1</li>
    <li id="tab2" onclick="chose_card(`tab2`)">Tab2</li>
    <li id="tab3" onclick="chose_card(`tab3`)">Tab3</li>
    <li id="tab4" onclick="chose_card(`tab4`)">Tab4</li>
    <li id="tab5" onclick="chose_card(`tab5`)">Tab5</li>
</ul>

<div class="content">
    <span class="chose" id="chose"></span>
</div>

<script>
    function chose_card(tab_no){
        document.getElementById("chose").innerHTML = `${tab_no}`.charAt(3).repeat(6);
    }
</script>
</body>
```
