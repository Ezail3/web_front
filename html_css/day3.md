## Ⅰ、常用元素与属性(一)

### 1.1 标题

h1-h6，1最大

```html
<div>
	<h1>一级标题</h1>
	<h2>二级标题</h2>
	<h3>三级标题</h3>
</div>
```

### 1.2 空格与换行

```html
<div>
    test</br>
    <div style="background: orange">
        &nbsp;&nbsp;&nbsp;test
    </div>
</div>
```

### 1.3 p标签

```html
<div style="background: blue;color: red;">
    <p style="text-indent: 2em">text</p>
</div>
```

p标签中只写文字，不要写其他任何东西

这个text会显示问红字，并且首行缩进2个字符

### 1.4 超链接

```html
<div>
    <a href="img/new.html" target="_blank">嘿嘿</a>
    <a href="https://www.baidu.com" target="_blank">呵呵</a>
</div>
```

第一个链接到本地html文件，第二个链接到百度

target属性决定这个链接以什么形式打开

### 1.5 引入图片

```html
<div style="text-align: center;">
    <img src="img/banner.jpg" title="图片标题" width="500px"/>
</div>
```

img元素自带宽高，只给宽或者高，大小会按比例自动缩放，固一般给其中一个即可

我们务必保证宽高比和原图一致

一般图片只缩小，不放大，放大会失真

图片居中不能用margin: auto 因为<img>不是块元素

要把它当作一个文本包起来实现居中

**img引入图片存在的问题**
一个banner图宽度很宽且样式中未设置宽度(设置了会按比例变化)，在小显示器上就会产生左右滚动条
一般也不会写死宽度，太宽或者太窄都不好,有人也许会像下面这样给<img>标签加一个父级div，给父级写死宽度
这也是不对的，如果banner图宽度比1200px要大，会溢出，在小显示器上还是有问题

```html
<div style="width: 1200px">
    <img>
</div>
```

**正解**

咱们用背景图片的方式引入图片，跨过<img>
只给一个原图片的高度即可

```html
<div style="background: url(img/banner.ipg) center; height: 600px;">
```

这样解决了左右滚动条问题，但是小显示器会看不到banner图两侧的内容，但这无伤大雅，一般设计那部分都是无关紧要的内容，嘿嘿
所以，这种比显示器大的图片建议用这种方式引入

### 1.6 文本属性

```html
<div style="width: 120px;
            height: 50px;
            background: lightblue;
            font-size: 18px;font-weight: bold;
            font-family: '微软雅黑';
            text-align: center; 
            line-height: 50px; 
            color: #ffffff">按钮</div>
```

这里写了一个按钮

text-align: center	文本左右对齐

line-height: 50px	和父级div保持高度一致，实现上下居中，这是让内联元素上下居中的一种方式，块元素有宽高，用不了这种方式

font-size: 18px	字体大小

font-weitht: bold	加粗，可接数字，数字越大，500等于没设置

font-family: '微软雅黑'	设置字体格式，用引号包住，外面有一层双引号，这里只能用单引号

### Ⅱ、小练习——写一个导航

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{margin: 0;padding: 0;}
        li{list-style: none;
            float: left;
            height: 50px;
            width: 120px;
            text-align: center;
            line-height: 50px;
            color: white;
            margin-left: 10px;
        }
        li:hover {background: orangered;
            cursor: pointer;
        }
        /*鼠标滑过li，background变为橘色，鼠标变为小手*/
        /*li:hover a{ color: oranged}
        鼠标划过li，a标签中的字变为橘色
	这种用法，只能控制划过内容的子集变化
        */	
        a{color: white; text-decoration: none;display: inline-block;height: 50px;width: 120px;}
    </style>
</head>

<body>
    <div style="background: #333333;">
        <ul style="width: 1200px; margin: auto">
            <li style="background: orangered">首页</li>
            <li><a href="http://www.baidu.com" target="_blank">关于我们</a></li>
            <li>客户案例</li>
            <li>新闻资讯</li>
            <li>我们的团队</li>
            <li>联系我们</li>
            <div style="clear: both;"></div>
        </ul>
    </div>
</body>
</html>
```

**tips: 页面布局的原则——不允许同一个层级的元素，即在同一行，又在同一列**
