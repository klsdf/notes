# http://127.0.0.1:8000/

# 服务器的基本代码

```javascript
var http = require("http");
var querystring = require("querystring")
var server = http.createServer(function(request,response){
	const methods = request.method;
	const url = request.url;
	const path = url.split('?')[0];
	const query = querystring.parse(url.split('?')[1]);

	response.setHeader("Content-Type","application/json;charset=utf-8");
	const resData = {
		methods,url,path,query
	}
	if(methods==='GET')
		response.end(JSON.stringify(resData));
	if(methods==='POST'){
		let postData = '';
		request.on('data',chunk=>{
			postData+=chunk.toString()
		})
		request.on('end',chunk=>{
			resData.postData=postData;
			response.end(JSON.stringify(resData));
		})
	} 
});

server.listen(8000,function(){
	console.log("服务器启动成功");
});
```

# 原生node搭建服务器

## 开发环境搭建

1. 在项目根目录初始化npm的环境

```shell
npm init -y
```

2. 在根目录下创建一个bin文件夹，里面放一个www.js
3. 修改package.json，把main修改成`bin/www.js`，这个是定义入口文件
4. 在www.js里面写服务器代码

```javascript
const http = require('http')
const POST = 8000
const serverHandle = require('../app.js')

const server = http.createServer(serverHandle)
server.listen(8000,function(){
	console.log("服务器启动成功");
})
```

5. 在根目录创建app.js文件，并写服务器配置的代码

```javascript
const serverHandle = (request,response)=>{
  //设置返回格式
  response.setHeader("Content-Type","application/json;charset=utf-8")

  response.end()
}
module.exports = serverHandle
```

6. 安装nodemon（自动重启服务器） 和cross-env

```shell
npm install nodemon cross-env --save -dev
```

7. 修改package.json的配置，之后可以直接用`npm run serve` 来运行项目（想念VUE。。。）

```javascript
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "serve": "cross-env NODE_ENV=dev nodemon ./bin/www.js"
},
```

## 初始化路由

1. 在根目录创建src目录
2. 在src目录中创建router目录，这个目录就是用来存放后端路由的，每个页面就是一个js文件
3. 在router文件夹里面创建需要的js文件，比如我需要博客页面和登录页面，那么我就创建blog.js和user.js

```javascript
//blog.js
const handleBlogRouter = (request, response) => {
  const method = request.method
  const url = request.url
  const path = url.split('?')[0]

  //获取博客列表
  if (method === 'GET' && path == '/api/blog/list') {
    return {
      msg: "博客列表"
    }
  }

  //获取博客详情
  if (method === 'GET' && path == '/api/blog/detail') {
    return {
      msg: "博客详情"
    }
  }

  //新建一篇博客
  if (method === 'POST' && path == '/api/blog/new') {
    return {
      msg: "新建博客"
    }
  }

  //删除一篇博客
  if (method === 'POST' && path == '/api/blog/delete') {
    return {
      msg: "删除博客"
    }
  }

  //更新一篇博客
  if (method === 'POST' && path == '/api/blog/delete') {
    return {
      msg: "更新博客"
    }
  }
}
module.exports = handleBlogRouter
```

```javascript
//user.js
const handleUserRouter = (request, response) => {
  const method = request.method
  const url = request.url
  const path = url.split('?')[0]

  //获取博客列表
  if (method === 'POST' && path === '/api/user/login') {
    return {
      msg: "用户登录"
    }
  }
}
module.exports = handleUserRouter
```

4. 把资源导入到app.js

```javascript
//app.js
const handleBlogRouter = require("./src/router/blog.js")
const handleUserRouter = require("./src/router/user.js")

const serverHandle = (request,response)=>{
  //设置返回格式
  response.setHeader("Content-Type","application/json;charset=utf-8")
  
  const blogData = handleBlogRouter(request,response)
  if (blogData){
    response.end(
      JSON.stringify(blogData)
    )
    return;
  }

  const userData = handleUserRouter(request,response)
  if (userData){
    response.end(
      JSON.stringify(userData)
    )
    return;
  }

  //如果以上的url都没有符合的，说明路径非法
  //1. 可以使用系统自带的404
  // response.writeHead(404,{"Content-type":"test/plain"})
  //2. 或者手动输入404
  response.end("404 NOT FIND ")
}
module.exports = serverHandle
```

## 建立model

1. 在src文件夹下面，建立model文件夹
2. 在里面创建resModel.js文件
3. 在里面写一些模块的代码

```javascript
class BaseModel {
  constructor() {

  }
  constructor(data, message) {
    if (typeof data == 'string') {
      this.message = data
      data = null
      message = null
    }
    if (data) {
      this.data = data
    }
    if (message) {
      this.message = message
    }
  }
}


class SuccessModel extends BaseModel {
  constructor(data, message) {
    super(data, message)
    this.errorNum = 0
  }
}

class ErrorModel extends BaseModel {
  constructor(data, message) {
    super(data, message)
    this.errorNum = -1
  }
}
```

## 建立dataHandle

这个文件夹里面，就是用来给router里面的那些接口返回具体数据的。

1. 在src文件夹下面，建立dataHandle文件夹
2. 在dataHandle中建立blog.js

```javascript
const getList = (author,keyword)=>{
  return [
    {
      id:1,
      name:"波莱特"
    },
    {
      id:2,
      name:"日日姬"
    }
  ]
}
```

## 在router中调用dataHandle

我们已经有了路由和数据控制的代码，现在要做的就是把两者结合，让路由跳转到的接口处理处理并返回

```javascript
const {getList} = require("../dataHandle/blog.js")
const {SuccessModel,ErrorModel} = require("../model/resModel.js")
const handleBlogRouter = (request, response) => {
  const method = request.method

  //获取博客列表
  if (method === 'GET' && request.path == '/api/blog/list') {
    const author = request.query.author || ''
    const keyword = request.query.keyword || ''
    const listData = getList(author,keyword)
    return new SuccessModel(listData)
  }

  //获取博客详情
  if (method === 'GET' && request.path == '/api/blog/detail') {
    return {
      msg: "博客详情"
    }
  }

  //新建一篇博客
  if (method === 'POST' && request.path == '/api/blog/new') {
    return {
      msg: "新建博客"
    }
  }

  //删除一篇博客
  if (method === 'POST' && request.path == '/api/blog/delete') {
    return {
      msg: "删除博客"
    }
  }

  //更新一篇博客
  if (method === 'POST' && request.path == '/api/blog/delete') {
    return {
      msg: "更新博客"
    }
  }
}
module.exports = handleBlogRouter
```

## 处理POST数据

```javascript
const querystring = require('querystring')
const handleBlogRouter = require("./src/router/blog.js")
const handleUserRouter = require("./src/router/user.js")

const getPostData = (request) => {
  const promise = new Promise((resolve, reject) => {
    if (request.method != 'POST') {
      resolve({})
      return;
    }
    if (request.headers['content-type'] !== 'application/json') {
      resolve({})
      return
    }
    else {
      let postData = '';
      request.on('data', chunk => {
        postData += chunk.toString()
      })
      request.on('end', () => {
        if (!postData) {
          resolve({})
          return
        }
        resolve(JSON.parse(postData))
      })
    }
  })
  return promise
}


const serverHandle = (request, response) => {
  //设置返回格式
  response.setHeader("Content-Type", "application/json;charset=utf-8")
  response.setHeader('Access-Control-Allow-Origin', '*')

  //获取公用path
  const url = request.url
  request.path = url.split('?')[0]

  //解析query
  request.query = querystring.parse(url.split('?')[1])

  // 处理postData
  // 把请求的数据放到请求体中
  getPostData(request).then(postData => {
    request.body = postData
    //处理路由
    const blogData = handleBlogRouter(request, response)
    if (blogData) {
      response.end(
        JSON.stringify(blogData)
      )
    return;
    }

    const userData = handleUserRouter(request, response)
    if (userData) {
      response.end(
        JSON.stringify(userData)
      )
      return;
    }
    response.end("404 NOT FIND ")
  })

}
module.exports = serverHandle
```

## 建数据库

```sql
DROP DATABASE IF EXISTS myblog;
CREATE DATABASE IF NOT EXISTS myblog;
CREATE TABLE USER(
	id INT AUTO_INCREMENT PRIMARY KEY,
	user_name VARCHAR(20) NOT NULL,
	PASSWORD VARCHAR(20) NOT NULL
);
CREATE TABLE blogs (
	id INT PRIMARY KEY AUTO_INCREMENT,
	title VARCHAR(50) NOT NULL,
	content LONGTEXT NOT NULL,
	create_time BIGINT	NOT NULL,
	author VARCHAR(20) NOT NULL
);

INSERT INTO USER(user_name,PASSWORD)
VALUE ('用户名','123456');

SELECT * FROM USER;

DELETE FROM USER
WHERE user_name="用户名";
```

## 连接数据库

首先安装插件

```shell
npm install mysql
```

然后写代码

```javascript
const mysql = require('mysql')

const con = mysql.createConnection({
  host:"localhost",//主机地址
  user:"root",//用户名
  password:"4399",//密码
  port:"3306",//端口号
  database:"myblog"//数据库名
})
//连接数据库
con.connect()

//执行sql语句
const sql = "SELECT * FROM USER;"
con.query(sql,(err,result)=>{
  if(err){
    console.error(err)
    return
  }
  else{
    console.log(result)
  }
})

//关闭连接
con.end()
```



## 目录结构

# Redis

## 安装

把文件夹复制到C盘根目录，并命名为redis，

打开一个 **cmd** 窗口 使用 cd 命令切换目录到 **C:\redis** 运行服务器：

```shell
redis-server.exe
```

然后另启一个 cmd 窗口，开启客户端

```
redis-cli
```



在项目中使用

```
npm intsall redis --save
```



## 使用

```
set 键 值
```

```
get 键
```

