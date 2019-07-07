## Ⅰ、ajax

异步向服务器发送请求，服务器返回部分数据，页面无刷新更改页面中部分内容

ajax的核心对象 XMLHttpRequest

IE版本的核心对象是XMLHTTP

### 1.1 使用步骤

```javascript
<script>
    	//地址：协议+域名+端口号+文件路径
    	//http www.baidu.com 80 /index.html
        //1.创建ajax核心对象
        var xmlhttp;
        if(window.XMLHttpRequest){
            xmlhttp = new XMLHttpRequest();
        }else{
            xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
        }
        //2.创建请求
        //xmlhttp.open(请求方式,请求地址,是否异步)
        xmlhttp.open("get","my.php?user=xxx&psd=xxx",true);
        //3.发送请求参数
        //格式：必须是"key=value&..."
        //post的请求参数写在send方法里面，如果请求方式为get，请求参数要写在请求地址后面，以?连接
	    //如果请求方式为post，要求open和send中间加一步设置请求头,如下：
        //xmlhttp.setRequestHeader("content-Type", "application/x-www-form-urlencoded");
        xmlhttp.send("user=xxx&psd=xxx");
        //get方式时send方法传null即可
        xmlhttp.send(null);
        //4.接收响应
        //readyState(当前请求状态)0尚未初始化，1正在发送请求，2请求完成，3正在相应，4相应完毕
        //status(服务器端返回的状态码)404找不到页面，200成功 302 304 500
        xmlhttp.onreadystatechange = function(){
            if(4 == xmlhttp.readyState && 200 == xmlhttp.status){
                var data = xmlhttp.responseText;
            }
        }
    </script>
```

### 1.2 get与post

get更快更简单，一般情况多用get

以下几种情况用post

- 发送包含未知的用户输入字符，更安全更稳定
- 发送大量数据，post没有数据量限制，get有

### 1.3 小练习

用ajax实现级联菜单

**html文件**

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <select id="province">
        <option>请选择省份</option>
    </select>
    <select id="city">
        <option>请选择城市</option>
    </select>

    <script>
        var xmlhttp;
        var province = document.getElementById("province");
        var city = document.getElementById("city");
        if(window.XMLHttpRequest){
            xmlhttp = new XMLHttpRequest();
        }else{
            xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
        }
        xmlhttp.open("get","province.php",true);
        xmlhttp.send(null);
        xmlhttp.onreadystatechange = function(){
            if(4 == xmlhttp.readyState && 200 == xmlhttp.status){
                var provinces = xmlhttp.responseText;
                var procincesArr = provinces.split(",");
                for(var i=0; i<procincesArr.length; i++){
                    var option = document.createElement("option");
                    option.innerHTML = procincesArr[i];
                    province.appendChild(option);
                }
            }
        }

        province.onchange = function (){
            city.innerHTML = "<option>请选择城市</option>";
            var provinceValue = province.value;
            xmlhttp.open("post","city.php",true);
            xmlhttp.setRequestHeader("content-Type", "application/x-www-form-urlencoded");
            xmlhttp.send("province="+provinceValue);
            xmlhttp.onreadystatechange = function(){
                if(4 == xmlhttp.readyState && 200 == xmlhttp.status){
                    var cities = xmlhttp.responseText;
                    var citiesArr = cities.split(",");
                    for(var i = 0; i<citiesArr.length; i++){
                        var option = document.createElement("option");
                        option.innerHTML = citiesArr[i];
                        city.appendChild(option);
                    }
                }
            }
        }
    </script>
</body>
</html>
```

**php文件**

province.php

```php
<?php
	echo "山东,广东"
?>
```

city.php

```php
<?php
	$pro=$_REQUEST["province"];
	if("山东"==$pro){
		echo "青岛,济南,威海";
	}else if("广东"==$pro){
		echo "深圳,广州,东莞,汕头";
	}
?>
```



## Ⅱ、JSON

```javascript
<script>
    var xmlhttp;
    if(window.XMLHttpRequest){
        xmlhttp = new XMLHttpRequest();
    }else{
        xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    xmlhttp.open("get","my.php","true");
    xmlhttp.send(null);
    xmlhttp.onreadystatechange = function(){
        if(4 == xmlhttp.readyState && 200 == xmlhttp.status){
            var data = xmlhttp.responseText;
            //解析json格式的字符串
            var data = JSON.parse(data);
            //方法2：用eval拼接括号也行
            //var data = eval("("+data+")")
            console.log(typeof(data));
            console.log(data.name);
        }
    }
</script>
```

my.php

```php
<?php
	echo '{"name":"小明","age":18}';
?>
```
