## Ⅰ、EventListener

之前一直使用的绑定事件的方法

```javascript
on+事件名 事件处理函数
```

当我想给一个元素同时绑定多个事件怎么办？

### 1.1 EventListener语法

```javascript
语法：obj.addEventListener("事件名","方法对象","是否在捕获阶段触发")
obj.removeEventListener("事件名","方法对象","是否在捕获阶段触发")
```

### 1.2 EventListener实例与注意点

```javascript
<div id="box">hello</div>
<script>
    function consoleMe(){
        console.log(1);
	}
	var box = document.getElementById("box");
	box.addEventListener("click",function(){alert(1);},false);
	box.addEventListener("click",consoleMe,false);
	box.removeEventListener("click",function(){alert(1);},false);//取消无效
	//特殊记：removeEventListener移除不了匿名函数
    //IE低版本(6以下)浏览器：
	//obj.attachEvent("事件处理函数名","方法对象")
    //obj.detachEvent("事件处理函数名","方法对象")
</script>
```



## Ⅱ、事件冒泡

### 2.1 事件触发周期

- 标准DOM：

  - 事件捕获	===>	目标触发	===》	事件冒泡

- IE

  - 事件触发	===》	事件冒泡	

    没有捕获阶段所以attachEvent没有是否在捕获阶段触发这个参数

### 2.2 事件冒泡演示

```javascript
<head>
	<style>
        .d1{width: 200px;height: 170px;background: black;margin: auto;padding-top: 30px;}
        .d2{width: 100px;height: 80px;background: green;margin: auto;padding-top: 20px;}
        .d3{width: 50px;height: 50px;background: blue;margin: auto;}
    </style>
</head>
<body>
	<div class="d1">
        <div class="d2">
            <div class="d3"></div>
        </div>
    </div>
	<script>
     	var divs = document.getElementsByTagName("div");
        for(var i=0; i<divs.length; i++){
            divs[i].onclick = function(){
                this.style.background = "yellow";
                alert(this.className);
                this.style.background = "";
            }
        }
    </script>
</body>
//点击d3，会触发3个div的事件，按d3 d2 d1的顺序触发
//事件捕获是从外往里 d1 d2 d3捕获到先记住不触发，直到找到目标，而事件触发是从里往外d3 d2 d1往外冒泡触发
//addEventListener方式来做这个测试，第三个参数设置为true，点击d3，则d1先变黄，事件捕获时触发
//火狐浏览器才可以测出来
```

### 2.3 阻止事件冒泡

```javascript
//标准dom：用一个事件对象来阻止
for(var i=0; i<divs.length; i++){
	divs[i].onclick = function(e){
		this.style.background = "yellow";
		alert(this.className);
		this.style.background = "";
		e.stopPropagation();
	}
}
//IE： e.cancelBubble = true;
```

### 2.4 进一步优化

```javascript
//this会跟着冒泡跑，指向不明确
//用事件对象里的target属性替换之,精确拿到事件源
for(var i=0; i<divs.length; i++){
	divs[i].onclick = function(e){
		e.target.style.background = "yellow";
		alert(e.target.className);
		e.target.style.background = "";
		//e.stopPropagation();
        //依然冒泡(alert依次打出d3 d2 d1)，但一直只是d3触发事件，不会往外跑
	}
}
```
