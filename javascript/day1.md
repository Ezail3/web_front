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

## Ⅱ、基本操作

### 2.1 控制台调试

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

### 2.2 注释

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

### 2.3 其他

1、javascript是单线程的，从上往下顺序执行

2、javascript包含ECMAScript、DOM、BOM，前两个是重点
