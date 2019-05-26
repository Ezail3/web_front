## Ⅰ、元素边距

### 1.1 外边距——margin

```html
<div class="box" style="margin-bottom: 20px">1</div>
<div class="box">2</div>
1元素下面加了20像素的栅栏把1和2隔开了

<div style="margin: 10px"></div>
表示四周都围起10px
margin: 10px 20px
表示上下10px，左右20px
margin: 10px 20px 30px 40px
表示上右下左
margin: auto
表示基于父元素居中，此时必须该元素必须设置宽度，不然会和父元素重合
```

**margin存在的问题**

```html
<div style="width: 500px;height: 500px; background: red;">
    <div style="width: 100px; height: 100px; background: blue;margin-left: 50px;margin-top: 50px"></div>
</div>
```

这段代码本意是让蓝色块在红色块内部，并且距离红色块左边框和上边框各10px，但结果只是实现了左边距离10px，而上面没有隔开，且红色块和蓝色块一起相对浏览器往下掉了50px，这个问题叫margin合并

用margin让子元素和父元素之间纵坐标方向隔开距离，会出现margin合并，即父子一起往下掉，两个元素谁的margin-top大就按哪个生效

### 1.2内边距——padding

鉴于margin在纵坐标方向存在合并问题，这里我们引申出内边距方案解决问题

```html
<div style="width: 500px;height: 500px; background: red;padding-top: 50px">
    <div style="width: 100px; height: 100px; background: blue;margin-left: 50px;"></div>
</div>
```

这里在红色块内部加了一个内边距进而实现了咱们的需求，padding用法和margin类似，此处不再重复

**padding存在的问题**

上面的代码看似解决了需求，其实是有问题的

细心观察，会发现这个红色块高了50px，变成了550px

这是因为盒模型，在使用内边距时会让内部容积变小，所以这里被默认加上了50px，所以我们需要单独处理，padding多少，元素宽高就要相应减去多少，如下:

```html
<div style="width: 500px;height: 450px; background: red;padding-top: 50px">
    <div style="width: 100px; height: 100px; background: blue;margin-left: 50px;"></div>
</div>
```

测试一波

```html
<div style="width: 500px;background: red; padding-top:50px;"></div>
```

这个红色块没有给高度，也没有子元素为其撑开高度，用了padding，它就显示了padding的高度

**小结：**

同级之间推荐用margin，子父级之间推荐用padding

## Ⅱ、元素定位——position

### 2.1 absolute

改变谁的位置就给谁加绝对定位，横纵坐标每个方向给一个位置即可定位

### 2.2 relative

以谁作参照物就给谁加相对定位，不给参照，会默认参照已经定位的父元素

定位时从里面往外定

**实现，蓝色在红色右下角，红色在绿色右上角**

蓝色在红色右下角，给蓝色加absolute，给红色加relative

红色在绿色右上角，给红色加absolute，给绿色加relative

此时发现红色加了两个position样式，后面覆盖前面，固第一个relative可以去掉，因为红色已经定位了，不给relative，里面的蓝色也能以它为参照，代码如下：

```html
<div style="width: 1200px;height: 1200px;background: green;position: relative">
    <div style="width: 800px;height: 800px;background: red;position: absolute;right: 0;top: 0">
        <div style="width: 100px; height: 100px; background: blue;position: absolute;right: 0;bottom: 0"></div>
    </div>
</div>
```



### 2.3 fixed

针对浏览器定位

```html
<div style="height: 5000px">
    <div style="width: 100px;height: 100px;position: fixed;right: 0;bottom: 0;background: red"></div>
</div>
```

上面这段滚动浏览器会发现红色块一直在页面右下角，不会变化，很常用

**定位存在的问题**

```html
<div style="background: yellow;">
    <div style="width: 200px;height: 200px;background: red;position: absolute;top: 0;left:0;"></div>
</div>
```

上面这段代码父元素显示不出来，是因为子元素用了定位，导致了它脱离文档流，无法为父元素撑开高度

```html
<div style="background: yellow;">
    <div style="height: 200px;background: red;position: absolute;top: 0;left:0;"></div>
</div>
```

这样写啥都见不着，脱离文档流，子元素没给宽度，无法继承父元素的宽度，父元素没给高度，无法被子元素撑开，一个道理

```html
<div style="background: yellow;">
    <div style="width: 200px;height: 200px;background: red;position: absolute;top: 0;left:0;"></div>
    <div style="width: 220px;height: 220px;background: green"></div>
</div>
```

上面这段黄色显示出来了，因为绿色块没定位，给他撑开了高度

但是发现滤色块呆在红色块底下，说明红色块没有占位置

**小结：**
定位元素存在不占位置和脱离文档流问题，无法解决，能用margin，padding就不要用定位
