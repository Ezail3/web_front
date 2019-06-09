## Ⅰ、javascript的引入与基本操作

### 1.1 两种方式引入javascript

- script标签形式

  放在<body>标签中最后部分，因为我们优先加载页面，后加载功能

  ```javascript
  <body>
  	...
  	<script>
  	</script>
  </body>
  ```

- 文件形式

  ```javascript
  <script src='js/index.js'>
  ```

  这个可以写在<body>体中，也可以写在<head>中的最后，一般写在<body>，写在<head>中需要用一个事件控制它页面加载完成后再加载

### 1.2、基本操作

**控制台调试**

- 输出

  ```javascript
  console.log(3)
  ```

- 弹窗

  ```javascript
  alert(3)
  ```

  和console的区别是，alert会自动带一个断点

- 不常用的输出，了解即可，没啥用

  ```javascript
  document.write(3)
  ```

**注释**

注释和css一样

- 当行注释

  ```javascript
  //单行注释
  ```

  

- 多行注释

  ```javascript
  /*
  多行
  注释
  */
  ```

**其他**

1、javascript是单线程的，从上往下顺序执行

2、javascript包含ECMAScript、DOM、BOM，前两个是重点


## Ⅱ、变量初识

内存 ===> 程序 ===》数据 ===》 变量

### 2.1 变量的使用

```javascript
var a = 3;	//声明 命名 初始化
console.log(a)	//使用
```

### 2.2 数据类型

javascript中有两大类数据类型，原始数据类型和引用数据类型，本节只介绍原始数据类型

原始数据类型的数据保存在栈中，一共有五种

- string

  字符串类型，使用时必须加引号

- number

  数字类型

- boolean

  布尔类型

- undefined

  变量声明后未初始化，默认村委undefined

- null

  空对象指针
