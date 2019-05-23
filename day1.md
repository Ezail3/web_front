## Ⅰ、引入CSS样式

### 1.1 内联样式

```html
<html>
    <head>
    </head>
    
    <body>
        <div style="width: 200px; height: 200px; background-color: deeppink"></div>
    </body>
</html>
```

### 1.2 外部样式

- 基于元素

```html
<html>
	<head>
        <style>
            div {width: 200px; height: 200px; background-color: deeppink}
        </style>
    </head>
    
    <body>
        <div></div>
    </body>
</html>
```

- 基于id

```html
 <html>  
	<head>
        <style>
        	#box {width: 200px; height: 200px; background-color: deeppink}
        </style>
    </head>

    <body>
        <div id="box"></div>
    </body>
</html>

元素id是唯一的，不可重复
```

- 基于class

```html
<html>
    <head>
        <style>
        	.box {width: 200px; height: 200px; background-color: deeppink}
        </style>
    </head>

    <body>
        <div class="box"></div>
        <div class="box"></div>
    </body>
</html>

元素class可重复

.a .b	表示父级class为a本身class为b的元素
.a, .b  表
示class为a和b的两种元素基于css文件
```

### 1.3 css文件

```html
<html>
    <head>
    	<link rel="stylesheet" href="./style.css">
    </head>
    
    <body>
          <div class="box"></div>
    </body>
</html>

./style.css文件(.表示和html同级，即一个目录中)
.box{width: 200px; height: 200px; background-color: deeppink}
```

**优先级**

- css从上往下执行，即同样的样式，后面覆盖前面
- !important(只对一个样式起作用) > 内联样式 > 外部样式(id>class) > css文件

## Ⅱ、元素分类

### 2.1 块元素

独占一行，默认有宽高，块元素可包含内联元素，常见块元素如下：

h、p、ul、ui、ol、oi、table、form、by、div

块元素若未设置宽度，则默认为其父级的100%

块元素默认高度不可省略(除非被子集元素撑开)

块元素实现一行内显示：浮动(基于父级)

```html
float:left
```

### 2.2 内联元素

不独占一行，默认无宽高，内联元素不可包含块元素，常见内联元素如下：

a、img、label、input、select、button、span

内联元素有宽高：显式指定(兼具内联和块的特点)

```html
display: inline-block
```

## Ⅲ、浮动注意点

### 3.1 不占位置

```html
<html>
    <head>
    	<style>
        	* {margin: 0; padding: 0;}
        	.box{width: 200px; height: 200px; background-color: deeppink; float: left}
    	</style>
	</head>

	<body>
        <div class="box">1</div>
        <div class="box">2</div>
        <div class="box">3</div>
        <div style="width: 600px; height: 300px; background-color: blue">666</div>
	</body>
</html>

此处666元素会被1、2、3三个元素遮挡住200px高度，也就是说这三个元素不占位置，666这个元素当他们不存在，直接基于body布局
```

### 3.2 脱离当前文档流

```html
<html>
    <head>
        <style>
            * {margin: 0; padding: 0;}
            .box{width: 200px; height: 200px; background-color: deeppink; float: left}
        </style>
	</head>

	<body>
    	<div style="background-color: yellow">
        	<div class="box">1</div>
        	<div class="box">2</div>
        	<div class="box">3</div>
    	</div>
	</body>
</html>

这个黄色div按道理是和1、2、3同样高，宽度和body一样，即和浏览器一样，但此处却显示不出来，原因是因为1、2、3使用了浮动，脱离文档流，已经脱离了黄色div，不属于它的子级，它无法给黄色元素撑开高度，所以无法显示
```

再看一例

```html
<html>
    <head>
	</head>

	<body>
    	<div style="width: 200px; height: 200px; background-color: deeppink">
        	<div style="height: 100px; background-color: blue; float: left"></div>
    	</div>
	</body>
</html>

此处蓝色块未设置宽度，默认与其父级一样为200px，但此处显示不出来，原因是蓝色块使用了浮动，脱离了粉红，都不认爹了，爹凭啥为你拉开宽度？
```

### 3.3 清除浮动

对于不占位置问题与脱离文档流的第一种情况(浮动元素无法撑开父级元素高度)可在一组浮动元素最后给一个清除浮动元素(和浮动元素同级)即可，如下：

```html
<div style="clear: both"></div>
```

而脱离文档流的第二种情况(浮动元素无法继承父级元素宽度)无法直接解决，务必直接将浮动元素宽度写死，不可缺省。
