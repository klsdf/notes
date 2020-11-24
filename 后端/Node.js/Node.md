# 概述

## 发展史

## Node.JS与Javascript

Node.js是遵循ECMAscript的语法规范，并在此基础上加入了一些node的api。而JavaScript是在ECMA的基础上，又加入了一些web api，这些web的api规范是由W3C制定的。

+ node.js 中使用的是[ECMAScript](https://baike.baidu.com/item/ECMAScript/1889420?fr=aladdin),也就是说他里面没有BOM,和DOM操作
+ node.js不是一种框架或者库,而是一种运行时环境
+ npm是世界上最大的开源库生态系统
+ 构建于chrome的V8引擎之上
+ JS是单线程的,因为多线程的话,网页渲染可能出现bug



#                      模块化

## 为什么有模块化

1. 提高代码复用率

开发多了就知道了,如果一个项目过大的话,动辄几万行,如果全放在一个文件,那别人来修bug岂不是爆炸,所以程序员们尽量把程序化成一个个小的部分,并且尽量减少彼此耦合,以便代码复用.

就比如说,同样一个导航栏,我这次写完,把他打包成一个模块,以后再开发网页,就可以直接拿过来用.

2. 防止变量作用域冲突

也就是防止变量重名,开发中,很多程序员都喜欢用一些常用的变量名,比如说index,buf,obj等等.那麻烦了,你这边叫buf,我那边也叫buf,那变量重名报bug,到底留谁的?打一架吗?

为了解决这个情况,Node会把每一个js文件打包成模块(其实就是封装成一个函数),使得里面的变量都是局部变量(有例外哦),这样,程序员们就可以开开心心起名字了。也就是说，**模块化之后，就没有全局作用域了，只有模块作用域。**

## 单个属性导入导出

### 向外暴露

```javascript
exports.a = 1;

exports.add = function(a,b){
  return a+b;
}
```

### 引用模块

```javascript
//一定要加require里面一定要加 ./
var md = require("./xxx.js");
console.log(md.a); 

var math = require("./xxx.js");
math.add(123,456);
```



## 多个属性导入导出

### 向外暴露

```javascript

module.exports = {
  defaultUrl:"/pages/developed/developed",
  RandomColor:function(){
    var colors = ["#bfc","#a4f","#DDA0DD","#40E0D0",
    "#B0C4DE","#008B8B","#F0E68C","	#FF8C00","#5F9EA0"];
    return colors[parseInt(Math.random() *colors.length)];
  }
}

```

### 引用模块

```javascript
const {defaultUrl,RandomColor} = require("../../../utils/util");
```



## 模块化的本质

  在node中,每个独立的js文件都是一个模块,这就意味着,除非使用exports暴露,任何变量都是局部变量.(除了声明真.全局变量).为什么会这样呢?实际上,node会把每一个js文件都封装成一个函数,如下所示

```javascript
function (exports, require, module, __filename, __dirname) {
	console.log(arguments.callee+"")
}
```

  用console把当前执行的函数打印出来,+""以便打印完整内容,可以看到,实际上js文件已经被封装了.
	
下面将依次说明各个参数的作用

1. **exports**: 

     用于暴露函数内的属性或者方法

2. **require**

     函数,用于引入外部模块

3. **module**

     代表模块自身,也就是说exports也是module的一个方法,可以用module.exports调用

4. **__filename**

   代表当前文件路径

5. **__dirname**

   代表当前文件所在文件夹的路径



## exports和module.exports的区别

在看具体的区别前,我们可以看一下这个例子.

```javascript
//exports.js文件
exports = { a:1 };
```

```javascript
//require.js文件
const nums = require("./exports.js")
console.log(nums.a);
```

之后编译器会打印**undefined**,这就很奇怪了,明明导出了一个对象,结果却提示没有定义?

这时,如果把exports文件略作修改

```javascript
//exports.js文件
module.exports = { a:1 };
```

现在,控制台就会正常打印1了.这是为什么呢?

其实exports和module.exports是指向同一片内存区域的.

第一种情况用代码来讲就是:

```c++
//系统默认把exports和module.exports指向一个地址 
int* module.exports = null;
int* exports = module.exports;
//此时 exports == module.exports
//接着exports = { a:1 }; 指针指向改变
exports = &a;
cout<<module.exports;
//所以module.exports里面还是啥都没有
```

第二种情况则是

```c++
//系统默认把exports和module.exports指向一个地址 
int* module.exports = null;
int* exports = module.exports;
module.exports = &a;
cout<<module.exports;
//此时正常打印
```

那为什么最上面那个单个属性导出就不用加module呢?

实际上可以类比于这个代码

```c++
//系统默认把exports和module.exports指向一个地址 
int* module.exports = null;
int* exports = module.exports;
*export = a;
//此时修改的指针指向的内容,所以module.exports正常运行
cout<<module.exports;
//此时正常打印1
```

**总结一下,导出对象的时候,必须使用module.exports,导出单个属性可以用exports**

## 详解require函数

require有两个作用

1. 加载并执行模块
2. 获取被加载模块的导出对象

### 1.加载并执行模块

#### 核心模块

加载核心模块直接写名字就可以了

```javascript
 require("http");
```

#### 用户自定义模块

加载用户自定义模块需要加"./" ,否则会被当做核心模块

```javascript
 require("./test.js");
```

其实加载这个文件的本质就是去执行url目录下的js文件


```javascript
//test.js文件中
consolo.log("test");
```


此时执行 `require("./test.js"); ` 控制台就会打印test

### 2.导入其他文件exports对象

可以通过`const xxx = require("./xxx.js");` 来导入其他文件中 `exports.xxx = 1;`  

## import和require

require导入模块是ES5的标准，import是ES6的标准。但是现在node和大多数浏览器没有广泛支持ES6，所以不建议使用import，如果非要使用的话，node中需要安装babel环境，浏览器中需要把标签设置为module。

```html
<!--浏览器环境-->
<script type="module">
    import {name} from './test.js';
</script>
```

node环境需要安装babel，在vue项目中可以直接安装，但是这里不演示了，直接使用ES5语法。

# 包 package

## 包的概述和结构

​	包就是node中打包好的一些模块,通常来说包应该具有以下结构

1. package.json：包描述文件

2. bin：用于存放可执行二进制文件的目录

3. lib：用于存放JavaScript代码的目录

4. doc：用于存放文档的目录

5. test：用于存放单元测试用例的代码

   其中package.json文件和lib最为重要,不可缺少.

## npm (Node Package Manager) 概述

NPM是随同NodeJS一起安装的包管理工具,用npm指令可以非常便捷的下载需要的包,无需手动安装,下载依赖等等.

也可以发布你自己创作的包.

**注意:npm中包的名字不能大写,不能使用驼峰法,请使用下划线代替**



### npm常用命令

- --save意味着在局部安装，也就是只安装在项目文件夹内
- -dev意味着开发依赖，也就是说在开发阶段使用的功能

要想执行npm命令,请先打开控制台,并提前cd到你的项目路径,以免把包装错地方

- npm	查看说明
- npm -v    查看版本号
- npm version   查看详细模块的版本号
- npm search xxxx    联网搜索xxxx相关的包,比如 npm search math
- npm init   在当前路径创建一个包
- npm install  xxx   在当前路径安装xxx包
- npm install xxx -g   在全局安装xxx包
- npm install  xxx --save   在安装包的同时,把这个包添加到你的项目依赖中.
- npm install xxx --save -dev 开发依赖，也就是说仅仅在开发阶段可以使用
- npm install   下载当前项目中的所有依赖包
- npm remove xxx  在当前路径删除xxx包
- npm



# Buffer

## 概述

Buffer是Node中自带的一种类，该类用来创建一个专门存放二进制数据的缓存区。因为JS本身没有二进制的数据类型,因此不能处理二进制文件,比如文件流之类的,这个Buffer可以极大增强JS的功能.

## 创建与使用

### 使用数据间接开辟空间


```javascript
const buf = Buffer.from("hello world");
console.log(buf);
```

因为Buffer是储存二进制文件的,所以里面的所有数据都会转化为二进制数据.

下面是打印的内容:

```Assembly
<Buffer 68 65 6c 6c 6f 20 77 6f 72 6c 64>
```
### 使用alloc方法直接开辟空间

```javascript
//创建10个字节的缓冲区
const buf = Buffer.alloc(10); 
//可以通过下标来访问每个字节
//可以使用16进制直接储存,也可以用十进制储存
buf[0] = 0x01;
buf[1] = 33;
//注意越界虽然不会报错,但是实际上会越界修改数据(有点像C语言),不要越界!!!
buf[10] = 123;
console.log(buf);
```

### 用write()方法写入数据

write方法会覆盖当前数据,并且会返回写入数据的个数.

```javascript
const buf = Buffer.from("hello");
let length = buf.write("world");
console.log(length,buf.toString()); 
```

输出结果为:

![image-20200901001024948](C:\Users\17966\AppData\Roaming\Typora\typora-user-images\image-20200901001024948.png)

## Buffer的常用方法

### 普通方法

- buf.toJSON();      当字符串化一个 Buffer 实例时,JSON.stringify() 会隐式地调用该 toJSON()
- buf.toString();     将当前Buffer 的内容转化为字符串类型.

### 静态方法

- Buffer.concat([buf1,buf2]);     注意参数里面是一个数组.

 ```javascript
  const buf1 = Buffer.from("hello");
  const buf2 = Buffer.from("world");
  const buf3 = Buffer.concat([buf1,buf2]);
  console.log(buf3.toString()); 
 ```

  


# path模块

## 获取分隔符

```javascript
const path = require("path");
//获取当前操作系统路径分隔符
console.log(path.sep);
//获取当前操作系统环境变量分隔符
console.log(path.delimiter);
```

**注意:在不同操作系统分隔符是不一样的.**

在windows里面,系统路径分隔符是\   环境变量分隔符是;

## 获取文件名的相关操作

```javascript
//获取带扩展名的当前文件名
console.log(path.basename(__filename));
//获取不带扩展名的当前文件名,注意后面的拓展名需要你自己改变
console.log(path.basename(__filename,".js"));
```



还记得__filename吗,在模块化本质讲过,忘了的话赶紧看一看,这句代码就是截取当前文件路径的最后一个文件名,也就是当前文件名.

```javascript
//获取当前文件夹所在路径
console.log(path.dirname(__filename));
//获取文件扩展名
console.log(path.extname(__filename));
```

**用join函数配合__dirname可以快速找到当前文件夹下面文件的绝对路径,非常好用!!!**

```javascript
console.log(path.join(__dirname,"text.txt"));
```



# fs 模块

fs是node中内嵌的一个核心模块,全称叫做file system,可以操作文件.

node中的文件操作均有同步和异步之分,异步方法最后一个参数都是回调函数,而同步方法一般就是在异步方法名字后面加个**Sync**,并且没有回调函数.

虽然异步函数写起来麻烦,但是推荐使用异步操作,因为快.

## 文件操作

### 获取文件信息

```javascript
//异步操作
const fs = require('fs');

fs.stat(__filename, function(err, stats) {
	if (err) {
		return console.error(err);
	}
	else if(stats){
	//stats 可以显示文件状态
	console.log(stats);
	console.log("读取文件信息成功！");

	// 检测文件类型
	console.log("是否为文件(isFile) ? " + stats.isFile());
	console.log("是否为目录(isDirectory) ? " + stats.isDirectory());
	}
})
```

```javascript
//同步操作
const fs = require('fs');

//打印文件状态
console.log(fs.statSync(__filename));

//检测文件类型
console.log("是否为文件(isFile)? "+fs.statSync(__filename).isFile());
console.log("是否为目录(isDirectory)? "+fs.statSync(__filename).isDirectory());
```

### 读文件

```javascript
const fs = require('fs');
fs.readFile('./test.txt', function(err, data) {
    // 读取文件失败/错误
  if (err) {
    console.error(err) ;
  }
    // 读取文件成功
	else if(data){
		//因为文件都是二进制的,所以会打印Buffer类型的数据
		console.log(data);
	}
});
```

结果如下:

![image-20200903120356308](C:\Users\17966\AppData\Roaming\Typora\typora-user-images\image-20200903120356308.png)

如果想看字符串的内容,可以用Buffer的toString方法.

### 写文件

node中写文件的操作,若你写入的文件不存在,那么系统会帮你创建一个,不过不能创建文件夹.

```javascript
const fs = require('fs');
//writeFile会覆盖原有的内容,而且若找不到文件,会自己创建一个文件
fs.writeFile("./test.txt", "hello world", (err) => {
  if (err) console.error(err) ;
  console.log('写入成功!');
});
```

之后本文件夹目录下的test.txt里面就会只有hello world,原内容会被覆盖掉.

但是若你不想覆盖原有的内容,可以用下面这个方法.

```javascript
const fs = require('fs');

fs.appendFile("./test.txt", "hello world", (err) => {
  if (err) console.error(err) ;
  console.log('写入成功!');
});
```



## 数据流操作

​	我们刚才所进行的文件操作都适用于比较小型的文件,因为读写文件时,编译器会把所有要操作的内容先缓存起来,

如果文件过大那么可能会导致响应太慢,或者内存不足.但是流操作是即时的,读取一个数据就会直接写入文件,体验更好.

### 读入流

```javascript
const fs = require('fs');

//建立读入流的通道
var readerStream = fs.createReadStream('test.txt');
//设置编码为 utf8。
readerStream.setEncoding('UTF8');
var data = "";
//当流中还有数据的时候,就会调用下面的函数,
//其中回调函数的chunk就是数据块的意思,也就是此时读到的数据
readerStream.on('data', function(chunk) {
   data += chunk;
});
//当流中数据流完时调用下面这个函数
readerStream.on('end',function(){
   console.log(data);
});
//发生错误调用下面这个
readerStream.on('error', function(err){
   console.log(err.stack);
});
```

### 写入流

```javascript
const fs = require('fs');
var data = "永远喜欢波莱特";

// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');
// 使用 utf8 编码写入数据
writerStream.write(data,'UTF8');
// 写入流必须手动关闭,之后会调用方下面那个finish的回调函数
writerStream.end();
// 写入流关闭后调用这个函数
writerStream.on('finish', function() {
    console.log("写入完成.");
});
//发生错误调用下面这个
writerStream.on('error', function(err){
   console.log(err.stack);
});
```

### 连通两个数据流

可读流的pipe方法可以复制文件,将可读流的内容流入可写流中.

```javascript
var writerStream = fs.createWriteStream('output.txt');
var readStream = fs.createReadStream('test.txt');
//将可读流的内容流入可写流中
readStream.pipe(writerStream);
```

## 目录操作

目录操作其实就是对文件夹的操作,刚才一直都是读写文件,现在我们可以创建删除文件夹了

### 创建文件夹

```javascript
const fs = require('fs');
const path = require("path");
fs.mkdir(path.join(__dirname,"testFolder"),function(err){
   if (err) 
       return console.error(err);
   console.log("目录创建成功。");
});
```

### 读取文件夹

```javascript
const fs = require('fs');
const path = require("path");
//读取当前路径下的文件夹,可以看到返回了一个数组,有各种你文件夹里面的文件
fs.readdir(path.join(__dirname),(err,files)=>{
   if (err) 
       return console.error(err);
   console.log(files);
});
```

### 删除文件夹

```javascript
const fs = require('fs');
const path = require("path");
fs.rmdir(path.join(__dirname,"testFolder"),(err,files)=>{
   if (err) 
       return console.error(err);
   console.log("删除成功");
});
```

可以看到我们刚才测试用的testFolder已经被删除了

# http 模块

## HTTP协议

Request消息的结构
- 请求行∶包括http请求的种类(GET或POST等,)请求资源的路径，http 协议版本
- 请求头:http头部信息
- 空行
- 请求体∶发送给服务器的query信息

Response消息的结构
- 状态行︰协议版本、状态码。
- 响应头∶响应头信息。
- 空行。
- 响应体∶响应请求的资源。

## 最简单的http服务

```javascript
var http = require("http");
//创建一个web服务器,返回一个serve实例
var server = http.createServer();
// 注册request请求事件
// 当客户端请求数据时,就会触发服务器的request请求,然后执行回调函数
server.on("request",function(request,response){
	console.log("收到客户端请求");
  //结束响应，否则网页打不开
  response.end();
})
//绑定端口号,启动服务器
//可以通过 http://127.0.0.1:8000/ 在浏览器打开
//默认80端口,不要使用默认端口,以免冲突
server.listen(8000,function(){
	console.log("服务器启动成功");
});
//可以关闭一下服务器
//serve.close();
```

最后可以用ctrl+c在终端关闭服务.

或者直接创建，推荐下面的这种：

```javascript
var http = require("http");
var server = http.createServer(function(request,response){
	console.log("收到客户端请求");
	response.end();
});

server.listen(8000,function(){
	console.log("服务器启动成功");
});
```



## request请求中回调函数的参数

当客户端请求数据时,就会触发服务器的request请求,然后执行回调函数,其实主要就是调用回调函数里面的response

```javascript
server.on("request",function(request,response){
  //request对象有一个url属性,可以输出当前的路径
	console.log("收到客户端请求,url为"+request.url);
	//response对象有一个write方法,可以给客户端发送响应数据
	// write可以使用多次,但是必须要有end结尾,否则客户端会一直等待响应
	response.write("hello world");
  //end函数可以选择传入一个参数
	response.end("again");
})
```

注意,response的响应内容只能是二进制数据或者字符串!!!!!!!!!!

## 响应内容的数据类型 Content-Type

还是刚刚那个代码,如果我现在把end里面换上中文,还能正常执行吗?

```javascript
server.on("request",function(request,response){
	response.write("hello world");
	response.end("你好,世界");
})
```
结果如下:

![image-20200830193110084](img\image-20200830193110084.png)

	为什么会出现乱码呢? 其实是因为response中不能正确解析中文的编码,我们在给客户端回应数据时,手动告诉浏览器,我们所用的编码格式.现在全世界通用的字符集是utf-8,我们自然也采用这个.

```javascript
server.on("request",function(request,response){
  response.setHeader("Content-Type","text/plain;charset=utf-8");
	response.write("hello world");
	response.end("你好,世界");
})
```

此时可以正常输出:

![image-20200830194904937](img\image-20200830194904937.png)



这时候你可能就会有疑问,明明说好了只用设置utf-8字符集的,现在怎末又来一个text/plain?原来啊,这个text就表明了你所响应数据的类型,后面那个代表采用什么编码格式.服务器响应的数据都是字符串或者二进制文件,为了准确告诉浏览器更多信息,我们需要手动添加类型.plain就代表了普通文本.

当然text类型不仅仅只有plain这一种,下面我将响应一段html代码.

```javascript
server.on("request",function(request,response){
  response.setHeader("Content-Type","text/html;charset=utf-8");
	response.end("<a href=''>hello world</a>");
})
```
此时浏览器将会以html的方式解析响应的内容

![image-20200830195747371](img\image-20200830195747371.png)

那么问题来了,这么多种资源,我怎么可能记得住到底使用什么指令呢?????不要怕,可以利用<a href="https://tool.oschina.net/commons">开源中国的工具网站</a>进行在线查询.



## 根据不同请求路径处理响应

```javascript
server.on("request",function(request,response){
  response.setHeader("Content-Type"," text/plain;charset=utf-8");

	//处理不同url
	var url = request.url;
	if(url=='/'){
		var loli=[
			{name:"巧克力"},
			{name:"椰子"}
		];
		response.end(JSON.stringify(loli));
	}
		
	else if(url=='/seTu')
		response.end("色图页");
	else
		response.end("404");
})

```

## 查看访问服务器的ip

```javascript
server.on("request",function(request,response){
	response.setHeader("Content-Type"," text/plain;charset=utf-8");
	//访问服务器的ip
	console.log("访问服务器的ip为"+request.socket.remotePort);

})

server.listen(800,function(){
	console.log("服务器启动成功");
});
```



# url模块

URL模块也是NodeJS的核心模块之一，用于解析url字符串和url对象

## 将url字符串转为对象

```javascript
let url = require("url")
let BilBilUrl = "https://www.bilibili.com/"
//parse可以把路径字符串解析成一个JS对象
let	BilBilObj = url.parse(BilBilUrl);
console.log(BilBilObj);
```

## url拼接

```javascript
let url = require("url")
let BaseUrl = "https://www.bilibili.com/"
let	Targeturl = ["36163336","/36163336","./36163336"]

for(let i =0;i<3;i++)
 console.log(url.resolve(BaseUrl,Targeturl[i]));
//答案都是
//https://www.bilibili.com/36163336
```



# 模板引擎

## 安装

```shell
npm install art-template --save
```

通过require使用

```javascript
var template = require("art-template")
```


