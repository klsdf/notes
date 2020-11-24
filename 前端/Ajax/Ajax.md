

# HTTP

HyperText Transfer Protocol（超文本传输协议）简称HTTP，

## HTTP的请求过程

1. DNS解析，把域名解析成ip地址
2. 建立TCP连接，三次握手
3. 服务器接收数据，并处理，返回
4. 客户端接收数据，进行页面渲染什么的

## 请求报文

由四部分组成，

1. 请求行
2. 请求头
3. 空行
4. 请求体

下面就是一个http请求的一个例子

```http
POST /test.html HTTP/1.1
Host: 127.0.0.1:8848
Connection: keep-alive

username=admin&password=null
```

### 请求头

格式如下

```http
请求方法 URL HTTP版本
```

比如

```http
POST /test.html HTTP/1.1
```

请求的方法为POST方法，访问的URL为/test.html，使用的协议版本为HTTP/1.1

### 请求行

### 请求体





## 响应报文

由四部分组成，

1. 响应行
2. 响应头
3. 空行
4. 响应体

```http
HTTP/1.1 200 OK
X-Powered-By: Express
x-timestamp: 1603966982798
x-sent: true
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Thu, 29 Oct 2020 10:07:19 GMT
Date: Thu, 29 Oct 2020 10:23:02 GMT
ETag: W/"146-17573d375e3"
Content-Type: text/html; charset=UTF-8
content-length: 615

<!DOCTYPE html>
<html>
	<head>
		<style>
			#out{
				perspective: 500px;
			}
			#in{
				width: 100px;
				height: 100px;
				background-color: #BC8F8F;
				transform: translate3d(0,0,60px);
			}
		</style>
	</head>
	<body>
		<div id="out">
			<div id="in">
				123
			</div>
		</div>
	<script>document.write('<script src="//' + (location.host || 'localhost').split(':')[0] + ':35929/livereload.js?snipver=1"></' + 'script>')</script><script>document.addEventListener('LiveReloadDisconnect', function() { setTimeout(function() { window.location.reload(); }, 500); })</script></body>
</html>
```

可以看到，响应体直接就是一个网页源码， 浏览器就是用这个来获取网页的。

### 响应头

格式如下

```http
HTTP版本 状态码 原因
```

### 响应行

### 响应体

## URL的结构



# express框架

**本框架基于node.js环境。**

## 安装

```shell
npm install express --save
```

## GET请求

### 后端

```javascript
//1.引入express
const express = require('express')
//2.创建应用对象
const app = express()
const port = 3000
//3.创建路由规则，如果接收到get请求，那么调用回调函数
//request是堆请求报文的封装
//response是对响应报文的封装
app.get('/', (request, response) => {
  //解决跨域问题
	response.setHeader('Access-Control-Allow-Origin', '*')
	response.send('Hello GET!')
})
//4.监听端口
app.listen(port, () => console.log(`${port} 已启动！`))
```

最后用node运行，运行服务器，进入对应的本地网页：127.0.0.1:3000

```shell
node .\test.js
```

### 前端

```html
<!DOCTYPE html>
<html lang="ch">
<head>
  <meta charset="UTF-8">
  <title>Ajax测试</title>
  <style>
    #content{
      margin-top: 10px;
      width: 300px;
      height: 200px;
      border: 1px black solid;
    }
  </style>
  <script>
    window.onload=function(){
      const btn = document.getElementById("btn")
      const ctn = document.getElementById("content")
      btn.onclick=()=>{
        //1.创建对象
        const xhr = new XMLHttpRequest()
        //2.初始化，设置请求方式和url
        xhr.open('GET','http://127.0.0.1:3000/')
        //3.请求体内容
        xhr.send()
        //4.事件绑定，返回后端结果
        //一共右4个state，直到4时，代表服务器把结果全部返回了
        xhr.onreadystatechange=()=>{
          if(xhr.readyState==4){
            if(xhr.status>=200 && xhr.status<300)
              console.log("状态码："+xhr.status)
              console.log("状态字符串："+xhr.statusText)
              console.log("所有响应头："+xhr.getAllResponseHeaders())
              console.log("响应体："+xhr.response)
              ctn.innerText=xhr.response
          }
        }
      }
    }
  </script>
</head>
<body>
  <button id="btn">加载页面</button>
  <div id="content"></div>
</body>
</html>
```

最后把页面运行到浏览器，一点按钮，就可以把本地服务器的内容请求到div里面了。（前提是你得先把服务器启动才行）

## POST请求

### 前端

```html
<!DOCTYPE html>
<html lang="ch">
<head>
  <meta charset="UTF-8">
  <title>前端网络请求</title>
  <style>
    #content{
      margin-top: 10px;
      width: 300px;
      height: 200px;
      border: 1px black solid;
    }
  </style>
  <script>
    window.onload=function(){
      const btn = document.getElementById("btn")
      const ctn = document.getElementById("content")
      btn.onclick=()=>{
        const xhr = new XMLHttpRequest()
        xhr.open('POST','http://127.0.0.1:8000/api/user/login')
        //请求体
        xhr.send('name=xxx&password=xxx')
        //设置响应类型
        xhr.responseType='json'
        xhr.onreadystatechange=()=>{
          if(xhr.readyState==4){
            if(xhr.status>=200 && xhr.status<300)
              ctn.innerText=xhr.response.name
          }
        }
      }
    }
  </script>
</head>
<body>
  <button id="btn">加载页面</button>
  <div id="content"></div>
</body>
</html>
```



### 后端

## 服务器响应JSON

### 前端

```html
<!DOCTYPE html>
<html lang="ch">
<head>
  <meta charset="UTF-8">
  <title>Ajax测试</title>
  <style>
    #content{
      margin-top: 10px;
      width: 300px;
      height: 200px;
      border: 1px black solid;
    }
  </style>
  <script>
    window.onload=function(){
      const btn = document.getElementById("btn")
      const ctn = document.getElementById("content")
      btn.onclick=()=>{
        const xhr = new XMLHttpRequest()
        xhr.open('GET','http://127.0.0.1:3000/')
        xhr.send()
        //设置响应类型
        xhr.responseType='json'
        xhr.onreadystatechange=()=>{
          if(xhr.readyState==4){
            if(xhr.status>=200 && xhr.status<300)
            //可以直接用对象的方式去访问json数据
              ctn.innerText=xhr.response.name
          }
        }
      }
    }
  </script>
</head>
<body>
  <button id="btn">加载页面</button>
  <div id="content"></div>
</body>
</html>
```

### 后端

```javascript
const express = require('express')
const app = express()
const port = 3000

var loli={
	name:"玲奈酱",
	age:100,
	type:"幼女"
}
//用JSON的方法，把对象转成JSON格式
var loliString = JSON.stringify(loli)
app.get('/', (request, response) => {
	response.setHeader('Access-Control-Allow-Origin', '*')
	response.send(loliString)
})
app.listen(port, () => console.log(`${port} 已启动！`))
```

## nodemon

我们之前如果修改了服务端代码，服务器是不会自动更新的，我们只能手动重启。为了方便操作，我们可以使用这个工具，自动更新服务器。

首先安装

```shell
npm install -g nodemon
```

之后用下面的代码执行js文件

```shell
nodemon .\文件路径.js
```

从此就不要再用`node`命令了。

## 网络请求超时与延时处理

### 前端

```html
<!DOCTYPE html>
<html lang="ch">
<head>
  <meta charset="UTF-8">
  <title>Ajax测试</title>
  <style>
    #content{
      margin-top: 10px;
      width: 300px;
      height: 200px;
      border: 1px black solid;
    }
  </style>
  <script>
    window.onload=function(){
      const btn = document.getElementById("btn")
      const ctn = document.getElementById("content")
      btn.onclick=()=>{
        const xhr = new XMLHttpRequest()
        //超时设置，单位为毫秒
        //服务器如果超过这个时间没有响应，那么请求自动取消
        xhr.timeout=2000;
        //超时回调函数，如果服务器超时响应超时则调用。
        xhr.ontimeout=function(){
          alert("网络异常！！！")
        }
        xhr.open('GET','http://127.0.0.1:3000/')
        xhr.send()
        xhr.onreadystatechange=()=>{
          if(xhr.readyState==4){
            if(xhr.status>=200 && xhr.status<300)
              ctn.innerText=xhr.response
          }
        }
      }
    }
  </script>
</head>
<body>
  <button id="btn">加载页面</button>
  <div id="content"></div>
</body>
</html>
```

### 后端

```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (request, response) => {
	response.setHeader('Access-Control-Allow-Origin', '*')
	//设置一个延时函数，3s后运行
	setTimeout(()=>{
		response.send("数据收到")
	},3000)
	
})

app.listen(port, () => console.log(`${port} 已启动！`))
```

## 取消网络请求

使用abort方法。

### 前端

```html
<!DOCTYPE html>
<html lang="ch">
<head>
  <meta charset="UTF-8">
  <title>Ajax测试</title>
  <style>
    #content{
      margin-top: 10px;
      width: 300px;
      height: 200px;
      border: 1px black solid;
    }
  </style>
  <script>
    window.onload=function(){
      const start = document.getElementById("start")
      const abort = document.getElementById("abort")
      const content = document.getElementById("content")
      let xhr = new XMLHttpRequest()
      //正常申请页面
      start.onclick=()=>{
        xhr.open('GET','http://127.0.0.1:3000/')
        xhr.send()
        xhr.onreadystatechange=()=>{
          if(xhr.readyState==4){
            if(xhr.status>=200 && xhr.status<300)
            content.innerText=xhr.response
          }
        }
      }
      abort.onclick=()=>{
        xhr.abort()
      }
    }
  </script>
</head>
<body>
  <button id="start">加载页面</button>
  <button id="abort">取消</button>
  <div id="content"></div>
</body>
</html>
```

### 后端

```javascript
const express = require('express')
const app = express()
const port = 3000


app.get('/', (request, response) => {
	response.setHeader('Access-Control-Allow-Origin', '*')
	//设置一个延时函数，3s后运行
	setTimeout(()=>{
		response.send("数据收到")
	},3000)
	
})

app.listen(port, () => console.log(`${port} 已启动！`))
```

之后可以在chrome的network中查看具体情况。

## 防止请求重复发送

其实原理很简单，就是设置一个开关，当发送数据时设置为开，发送完设置为关就行了。

如果发送数据时遇到新的请求，那么自动放弃之前的，用新的。

### 前端

```html
<!DOCTYPE html>
<html lang="ch">

<head>
  <meta charset="UTF-8">
  <title>Ajax测试</title>
  <style>
    #content {
      margin-top: 10px;
      width: 300px;
      height: 200px;
      border: 1px black solid;
    }
  </style>
  <script>
    window.onload = function () {
      const start = document.getElementById("start")
      const content = document.getElementById("content")
      let xhr = new XMLHttpRequest()
      let isSending = false
      //正常申请页面
      start.onclick = () => {
        if(isSending==true)
          xhr.abort()
        xhr.open('GET', 'http://127.0.0.1:3000/')
        xhr.send()
        xhr.onreadystatechange = () => {
          if (xhr.readyState == 4) {
            isSending=false
            if (xhr.status >= 200 && xhr.status < 300)
              content.innerText = xhr.response
          }
        }
      }
    }
  </script>
</head>

<body>
  <button id="start">加载页面</button>
  <div id="content"></div>
</body>

</html>
```

### 后端

```javascript
const express = require('express')
const app = express()
const port = 3000


app.get('/', (request, response) => {
	response.setHeader('Access-Control-Allow-Origin', '*')
	//设置一个延时函数，3s后运行
	setTimeout(()=>{
		response.send("数据收到")
	},3000)
	
})

app.listen(port, () => console.log(`${port} 已启动！`))
```

# http://httpbin.org/

这个网站可以来模拟各种响应

# Axios

## 安装

```shell
npm install axios --save
```



```javascript
axios({
  url: '',
  method: 'post',
  params:{}
  //请求体参数
  data:{}
  //请求头
  headers:{}
}).then(response => {
  console.log('请求结果：', response);
});
```

