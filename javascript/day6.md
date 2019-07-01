## Ⅰ、定时器概念

定时器是让网页自动运行的唯一办法

定时器分为一次性定时器和周期性定时器

### 1.1 一次性定时器

等待一定的时间后做某件事情

```javascript
setTimeout(干啥事,等待毫秒数)
//干啥事可以是匿名函数，也可以是函数名
setTimeout(function(){console.log(1)},2000);
//等价于
setTimeout(my,2000);
function my(){
    console.log(1);
}
```

### 1.2 周期性定时器

每隔一段时间做某件事情

```javascript
setInterval()
//同一次性定时器
```

每个方法都需要一个对象去调用它，定时器属于window的方法，由window调用它

### 1.3 停止定时器

```javascript
//clserTimeout()
//clearInerval()
var timer = null;
timer = setInterval(function(){consol.log("hello")},1000);
//打印出来是1，定时器中，变量是用来存线程号的，这个1是线程号，clearInterval(1)也能玩
console.log(timer);
clearInterval(timer) timer=null;
```



## Ⅱ、this

js中的thiis，指向函数运行时所在的对象， 换言之，谁调用了函数my()，my()中的this就指向谁

```javascript
<body>
    <div class="box">hello</div>
	<div class="box">world</div>
	<div class="box">bye</div>
</body>
<script>
    var box = document.getElementsByClassName("box");
    for(var i = 0; i < box.length; i++){
        box[i].onclick = function(){
            alert(this.innerHTML);
        }
    }
</script>
//我点谁(谁调用function这个方法)，this就是谁
//换成老式写法
<body>
    <div class="box" onclick="my(this)">hello</div>
	<div class="box" onclick="my(this)>world</div>
	<div class="box" onclick="my(this)>bye</div>
</body>
<script>
	function my(m){
        alert(m.innerHTML)
    }
</script>
//此时在标签中绑定事件并传入参数this，这时候的this就是这个标签对象
```



**重点：所以在定时器中的方法用到this，这个this指window**

```javascript
window.setInterval(function(){this}, 1000)
//定时器中的this永远指向window
```



## Ⅲ、多线程

定时器是一个多线程的程序

每个定时器是一个独立的线程，互不干扰

一个进程里有多个线程



## Ⅳ、案例

### 4.1 倒计时 今日十二点

```javascript
<body>
    <h1 id="txt"></h1>
    <script>
        var txt = document.getElementById("txt");
        function calc(){
            var target = new Date("2019-7-2 1:22:00");
            var now = new Date();
            var ms = target - now;
            var h = Math.floor(ms/1000/60/60);
            var m = Math.floor((ms - h*60*60*1000)/1000/60);
            var s = Math.floor((ms - h*60*60*1000 - m*60*1000)/1000);
            txt.innerHTML = `距离秒杀开始还有${h<10?"0"+h: h}时${m<10?"0"+m: m}分${s<10?"0"+s: s}秒`;
            if(ms < 0){
                clearInterval(timer);
                timer = null;
                txt.innerHTML="Bingo~~~"
            }
        }

        var timer = null;
        timer = setInterval(calc,1000);
    </script>
</body>
```

### 4.2获取验证码

```javascript
<body>
    <div>
        <input type="text" placeholder="请输入验证码"/>
        <button id="btn" style="width: 120px;cursor: pointer" onclick="myclick()">获取验证码</button>
    </div>
    <script>
        var btn = document.getElementById("btn")
        function myclick(){
            var last_time = 3;
            var timer = null;
            timer = setInterval(function(){
                last_time--;
                if(last_time < 0){
                    clearInterval(timer);
                    btn.innerHTML = "获取验证码";
                    btn.style.backgroundColor = "white";
                    btn.style.cursor = "point";
                    btn.disabled = false;
                }else{
                    btn.innerHTML = `${last_time}秒后重新获取`;
                    btn.style.backgroundColor = "grey";
                    btn.style.color = "black";
                    btn.style.cursor = "default";
                    btn.disabled = true;
                }
            },1000)
        }
    </script>
</body>
```

### 4.3 小广告

```javascript
<body>
    <div id="adv">
        <span onclick="hide()">关闭</span>
    </div>
    
    <script>
        //2s完成 33ms/次 位移3px/次
        //3个方法，往上走，往下走，关闭
        var adv = document.getElementById("adv");
        function up(){
            var cssStyle = document.defaultView.getComputedStyle(adv,null);
            var bot = parseInt(cssStyle.bottom);
            //console.log(bottom) 直接获取css的样式只能获取内联样式的css，所以要通过上面一步先获取元素所有css样式
            if(0 != bot){
                bot += 3;
                adv.style.bottom = bot + 'px';
            }else{
                clearInterval(timer);
                timer = null;
            }
        }

        function down(){
            var cssStyle = document.defaultView.getComputedStyle(adv,null);
            var bot = parseInt(cssStyle.bottom);
            //console.log(bottom) 直接获取css的样式只能获取内联样式的css，所以要通过上面一步先获取元素所有css样式
            if(-180 != bot){
                bot -= 3;
                adv.style.bottom = bot + 'px';
            }else{
                clearInterval(timer);
                timer = null;
                timer2 = setTimeout(function(){timer = setInterval(up,33)},3000);
            }
        }

        function hide(){
            clearInterval(timer);
            timer = null;
            //往上走还没结束就点了关闭的处理
            timer = setInterval(down,100);
        }
        var timer = null;
        var timer2 = null;
        window.onload = function(){
            timer = setInterval(up,33)
        };
    </script>
</body>
```
