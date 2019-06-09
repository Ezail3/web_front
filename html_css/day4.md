## Ⅰ、常用元素与属性(二)

### 1.1 画圆

画圆很简单，其实就是给正方形的四个角加弧度即可，直接加到边长的一半就成了圆形

```html
<div style="width: 200px;height: 200px;background-color: red; border-radius: 100px"></div>
```

**描边**

- solid——实线

- dashed——虚线

```html
    <div style="width: 200px;height: 200px;border-radius: 100px;border: orange 2px solid"></div>
    <div style="width: 200px;height: 200px;border-radius: 100px;border: purple 2px dashed"></div>
```

### **描边存在的问题**

```html
    <div style="width: 200px;height: 200px;border-radius: 100px;border: red 2px solid"></div>
    <div style="width: 200px;height: 200px; border-radius: 100px;background-color: red;"></div>
```

会发现上面的圆稍微比下面的圆要大一点点，

原因是描边是加在外面，加一个属性解决如下：

```html
<div style="width: 200px;height: 200px;border-radius: 100px;border: red 2px solid;box-sizing: border-box"></div>
```

### 1.2 上下左右居中

最基本的解决方案如下：

```html
<div style="width: 500px;height: 500px;position: absolute;top: 50%;left: 50%;background: red;margin-top: -250px;margin-left: -250px;"></div>
```

还可以使用灵活布局，一个css就解决，这里先不说

### 1.3 输入框——表单元素

```html
<form>
	<input type="text" placeholder="用户名" name="user_name">
    <br>
    <input type="password" placeholder="密码" name="password">
    <br>
    <input type="button" value="按钮">
</form>

 <br>
 <button style="width: 160px;height: 54px;background: #5696ff;color: #fff;font-size: 26px;border: none;outline: none">按钮</button>
<!--表单元素都虽然是内联元素，但都可以设置宽高-->
```

输入框居中方案：

将输入框包在一个同样大小的<div>中，对<div>做margin: auto

**写个输入框玩一下**

```html
<body style="background-color: rgb(240,243,239)">
    <div style="width: 400px;margin: auto;margin-top: 30px;opacity: 0.5;">
        <input type="text" placeholder="请输入您想要搜索的内容" style="width: 395px;height: 30px;padding-left: 5px;border: none;outline: none">
    </div>
</body>
```



### 1.4 透明块

opacity值在0到1之间，越小透明度越高

```html
<div style="height: 100px; width: 100px;background-color: purple;opacity: 0.5;"></div>
```

## Ⅱ、查漏补缺

### 2.1 投影

```html
<div style="width: 500px;height: 500px;background: white;box-shadow:#999999 0px 0px 20px 20px;margin: auto;margin-top: 200px;"></div>
<!--投影颜色 水平偏移距离，上下偏移距离，模糊程度(值越大越模糊)，投影大小 -->
<!--文字投影用text-shadow,只给三个px,少一个投影大小-->
```

### 2.2 表格

```html
<table style="width:600px; margin: auto;border: 1px solid;border-collapse: collapse">
    <tr style="background: darkgray">
        <td>编号</td>
        <td>姓名</td>
        <td>年龄</td>
    </tr>
    <tr>
        <td>1</td>
        <td>Ezail</td>
        <td>19</td>
    </tr>
    <tr>
        <td rowspan="2" colspan="2">2</td>
        <td>Allen</td>
    </tr>
    <tr>
        <td>Kobe</td>
    </tr>
</table>
```

### 2.3 超出部分隐藏

标签中，字母和数字溢出的话，不会换行，所以要隐藏

```html
<p style="width: 50px;height: 50px;background: red;overflow: hidden;text-overflow: ellipsis">aaaaaaaaaaaaaaaaaaaaaaaaaaaaa</p>
```

这俩属性必须同时出现才能生效

**两个块的超出隐藏**

```html
<div style="width: 500px;height: 500px;background: green;overflow: scroll">
    <div style="width: 1000px; height: 200px;background: red"></div>
</div>
```

scroll意思是以滚动条的形式展示

### 2.4 文字强制不换行

标签中，文字溢出会换行

```html
<button style="width: 50px;white-space: nowrap">59s后重新获取</button>
```
