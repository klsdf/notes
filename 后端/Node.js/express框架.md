# 说明

1. 本文技术框架为node+express+mysql

# 准备工作

## 安装脚手架

全局安装（已经安装过的不用安）

```shell
npm install express-generator -g
```

然后在需要的目录下创建项目文件夹

```shell
express 项目文件夹的名字
```

然后进入创建的文件夹

```shell
 cd 文件夹名
```

安装项目依赖

```shell
npm install
```

启动项目

```shell
 npm start  
```

## 安装nodemon和cross-env

```shell
npm install nodemon cross-env --save -dev
```

然后在package.json的script后面再加一条

```javascript
"serve": "cross-env NODE_ENV=dev nodemon ./bin/www.js"
```

然后以后就可以用serve来运行项目

```shell
npm run serve
```

## 安装mysql和xss

注意！需要拥有mysql环境

```shell
 npm install mysql xss --save
```



## 安装express-session

```shell
 npm install express-session --save
```

## 安装redis

注意！需要拥有redis环境

```shell
npm install redis connect-redis --save
```

## 安装http-server

安装过的可以不用再装了

```shell
npm install http-server -g
```



## Postman

这个不需要安装，直接下载就能用

https://www.postman.com/downloads/



## 在浏览器打开

默认的端口号是3000，所以可以直接在本地浏览器打开http://127.0.0.1:3000/

打开之后会默认出现一个express的页面

## 建数据库

mysql打开，直接粘过去。

```sql
DROP DATABASE IF EXISTS TwoDimensions;
CREATE DATABASE IF NOT EXISTS TwoDimensions;
USE TwoDimensions;

CREATE TABLE food(
	id INT AUTO_INCREMENT PRIMARY KEY,
	food_name VARCHAR(20),
	price FLOAT
);

CREATE TABLE girls(
	id INT  AUTO_INCREMENT PRIMARY KEY,
	loli_name VARCHAR(20) UNIQUE,
	age INT NOT NULL,
	nature ENUM('傲娇','天然呆','病娇','三无','腹黑','元气','工口','温柔','高冷') DEFAULT '傲娇',
	favorite_food_id INT,
	CONSTRAINT fk_girls_food FOREIGN KEY(favorite_food_id) REFERENCES food(id)
);

CREATE TABLE users(
	`username` VARCHAR(20) PRIMARY KEY,
	`password` VARCHAR(20)
);


INSERT INTO food
VALUE (NULL,'蛋包饭',17.5),
	  (NULL,'拉面',10),
	  (NULL,'面硬加咸蔬菜加倍蒜末和油多多',24.7),
	  (NULL,'咖啡',20),
	  (NULL,'蛋糕',50),
	  (NULL,'奶茶',7),
	  (NULL,'鱼香肉丝',21.4),
	  (NULL,'宫爆鸡丁',24.9),
	  (NULL,'糖醋里脊',34),
	  (NULL,'老陕肉夹馍凉皮和冰峰',30),
	  (NULL,'老食堂二楼咖喱饭',13),
	  (NULL,'老食堂一楼黄桥烧饼',8),
	  (NULL,'小吃街冒菜',15.5),
	  (NULL,'不可描述的南极洲糖',9999);

	  
INSERT INTO girls
VALUE (NULL,'巧克力',14,'元气',1),
	  (NULL,'香子兰',19,'三无',1),
	  (NULL,'桂',23,'工口',2),
	  (NULL,'枫',23,'傲娇',2),
	  (NULL,'红豆',14,'傲娇',8),
	  (NULL,'椰子',19,'傲娇',2),
	  (NULL,'艾米利亚',23,'傲娇',12),
	  (NULL,'雷姆',18,'温柔',2),
	  (NULL,'拉姆',18,'傲娇',6),
	  (NULL,'亚丝娜',20,'温柔',2),
	  (NULL,'诗音',17,'高冷',2),
	  (NULL,'莉兹贝特',28,'傲娇',10),
	  (NULL,'西莉卡',16,'傲娇',2),
	  (NULL,'结衣',2,'傲娇',8),
	  (NULL,'莉法',18,'傲娇',2),
	  (NULL,'由纪',20,'傲娇',7),
	  (NULL,'爱丽丝',18,'傲娇',9),
	  (NULL,'朝武芳乃',19,'傲娇',NULL),
	  (NULL,'常陆茉子',19,'傲娇',NULL),
	  (NULL,'最可爱的小丛雨',300,'傲娇',8),
	  (NULL,'蕾娜',20,'傲娇',4),
	  (NULL,'鞍马小春',16,'傲娇',2),
	  (NULL,'马庭芦花',23,'傲娇',7),
	  (NULL,'绫地宁宁',18,'傲娇',3),
	  (NULL,'因幡爱瑠',17,'傲娇',2),
	  (NULL,'椎叶䌷',16,'傲娇',9),
	  (NULL,'户隐憧子',20,'傲娇',10),
	  (NULL,'仮屋和奏',19,'傲娇',2),
	  (NULL,'沢井夏叶',7,'傲娇',13),
	  (NULL,'有岛爱丽丝',16,'傲娇',6),
	  (NULL,'栖美',18,'傲娇',2),
	  (NULL,'八六',120,'温柔',NULL),
	  (NULL,'右田日日姬',23,'傲娇',2),
	  (NULL,'我老婆雏衣波莱特',26,'温柔',NULL),
	  (NULL,'玲奈',70,'傲娇',5),
	  (NULL,'右田真闇',26,'傲娇',1),
	  (NULL,'宝生稀咲',22,'傲娇',8),
	  (NULL,'蓑笠凪',13,'傲娇',9),
	  (NULL,'早濑深美',14,'傲娇',7),
	  (NULL,'牧濑红莉栖',23,'傲娇',6),
	  (NULL,'椎名真由理',20,'天然呆',4),
	  (NULL,'漆原琉华',21,'傲娇',10),
	  (NULL,'阿万音铃羽',23,'傲娇',11),
	  (NULL,'菲利斯·喵喵',12,'傲娇',12),
	  (NULL,'天王寺绹',12,'傲娇',11),
	  (NULL,'阿万音由季',20,'傲娇',9),
	  (NULL,'高坂桐乃(陈睿叔叔)',18,'傲娇',7),
	  (NULL,'田村麻奈实',19,'傲娇',6),
	  (NULL,'槙岛沙织',19,'傲娇',5),
	  (NULL,'五更琉璃',18,'傲娇',4),
	  (NULL,'新垣绫濑',18,'病娇',8),
	  (NULL,'来栖加奈子',15,'傲娇',10),
	  (NULL,'赤城濑菜',19,'傲娇',13);
```



# 建立路由

## 写路由处理

在根目录有一个routes文件夹，这个里面放着的都是路由处理的文件，根据不同url，需要写不同逻辑的处理代码。

里面默认有index.js和users.js，这两个如果不需要可以删除。我们直接使用自己的路由。

首先，在routes下面建立路由名称，比如我想要建立一个首页的路由，所以我就可以起名home。

之后，在下面把这个代码粘过去

```javascript
var express = require('express');
var router = express.Router();

/* 注意这个路径并不是指根路径，路径问题中有详细解释 */
router.get('/', function(req, res, next) {
  res.render('index', { title: '首页' });
});

module.exports = router;

```

## 导入自定义路由

在app.js中的最上面可以发现发现这样两行代码，可以删掉

```javascript
var indexRouter = require('./routes/index');
var usersRouter = require('./routes/users');
```

之后加上我们自己所写的路由

```javascript
var homeRouter = require('./routes/home.js');
```

## 建立路由关系

最后就是来实际引用，可以在app.js中间部分找到下面两行代码

```javascript
app.use('/', indexRouter);
app.use('/users', usersRouter);
```

此时可以把这个删掉，替换成我们的

```javascript
app.use('/', homeRouter);
```

## 测试

此时点入http://127.0.0.1:3000/，就可以看到首页的欢迎界面了。

![image-20201106183416400](img/image-20201106183416400.png)

## 路径问题

注意，在这个express的脚手架里面，为了解耦合，路由的路径都是分开写的，最后会拼在一起。

比如说`/index/setu`这个路径，可以有多种写法

```javascript
//app.js中
app.use('/inddex', indexRouter);
//index.js
router.get('/setu', function(req, res, next) {
  res.render('index', { title: '首页' });
});


//或者

//app.js中
app.use('/inddex/setu', indexRouter);
//index.js
router.get('/', function(req, res, next) {
  res.render('index', { title: '首页' });
});
```

也就是说又app.js中处理大的父路径，再由具体路由处理子路径。

这样子的好处就是，以后要是父路径发生了变化，子路径不受影响。并且一个大的父路径下分多个子路径也更有可读性，不然一个文件把所有的url都列出来会显得非常繁琐。

## 返回数据

接下来让我们看看如何返回真正的数据。

express支持直接返回json类型的数据，当然了原生是不支持的。。。

### GET

```javascript
router.get('/testGetApi', function(req, res, next) {
  res.json({
    language:"C++",
    difficult:"hard"
  });
});
```

### POST

express可以直接解析请求体的数据，我们可以直接把请求体的数据拿到                                                                                                                                                           

```javascript
router.post('/testPostApi', function (req, res, next) {
  const { language, difficult } = req.body
  console.log(language,difficult)
  res.json({
    language,difficult
  });
});
```

## *中间件

这个属于额外进阶内容，选修。



# 连接硬件数据库

以MySql为例

## 设置数据库配置

1. 在根目录下创建一个config文件夹，用来存放各种神秘配置。

2. 然后创建一个db.js，用来配置数据库
3. **这个里面的用户名和密码需要写自己的**

```javascript
const env = process.env.NODE_ENV  // 环境参数

// 配置
let MYSQL_CONF
let REDIS_CONF

if (env === 'dev') {
  // mysql
  MYSQL_CONF = {
    host: "localhost",//主机地址
    user: "root",//用户名
    password: "4399",//密码
    port: "3306",//端口号
    database: "twodimensions"//数据库名
  }

  // redis
  REDIS_CONF = {
    port: 6379,
    host: '127.0.0.1'
  }
}

if (env === 'production') {
  // mysql
  MYSQL_CONF = {
    host: "localhost",//主机地址
    user: "root",//用户名
    password: "4399",//密码
    port: "3306",//端口号
    database: "twodimensions"//数据库名
  }

  // redis数据库，后面会讲
  REDIS_CONF = {
    port: 6379,
    host: '127.0.0.1'
  }
}

module.exports = {
  MYSQL_CONF,
  REDIS_CONF
}
```

## 连接并运行

1. 在根目录创建一个database的文件夹，这个文件夹是用来建立数据库连接，并且进行增删改查操作的。
2. 在这个文件夹内创建mysql.js文件，用来处理mysql的数据库。然后写代码。

```javascript
const mysql = require('mysql')
const { MYSQL_CONF } = require('../config/db')

// 创建链接对象
const con = mysql.createConnection(MYSQL_CONF)

// 开始链接
con.connect()

// 统一执行 sql 的函数
function exec(sql) {
    const promise = new Promise((resolve, reject) => {
        con.query(sql, (err, result) => {
            if (err) {
                reject(err)
                return
            }
            resolve(result)
        })
    })
    return promise
}

module.exports = {
    exec,
    escape: mysql.escape
}
```

## 处理数据

1. 在根目录下创建一个data_handle的文件夹，用于处理数据库的数据，**说白了就是在这里写sql语句**
2. 在文件夹里面创建girls.js，这个文件夹下的文件名和routes下面的是一样的，因为这个文件夹就是用于处理数据的，之后会把数据发给路由。
3. 写代码

```javascript
const xss = require('xss')
const { exec } = require('../database/mysql')

const getGirls = (id, name) => {
    let sql = `select * from girls where 1=1 `
    if (id) {
        sql += `and id ='${id}' `
    }
    if (name) {
        sql += `and name like '%${name}%' `
    }
    sql += `order by age desc;`

    // 返回 promise
    return exec(sql)
}

module.exports = {
  getGirls
}
```

## 测试

新建一个接口：http://127.0.0.1:3000/girls，创建接口的方法刚才说过了，我们只看一下最核心的。

在routes中创建girsl.js文件

```javascript
var express = require('express');
var {getGirls} = require('../data_handle/girls.js')

var router = express.Router();

router.get('/', function (req, res, next) {
  const id = req.query.id || ''

  const result = getGirls(id)

  return result.then(data => {
    res.json(data)
  })
});
module.exports = router;
```

之后就可以访问到数据库的数据啦，还可以用查询字符串来指定内容

http://127.0.0.1:3000/girls?id=2

![image-20201106204935164](img/image-20201106204935164.png)

# 用户登录与注册

## 前提准备

### 引入session

这个是用来验证用户登录信息的。

在app.js最上面

```javascript
const session = require('express-session')
```

然后在下面加入app.use，这个代码要在use路由之前，因为先要处理登录信息才能处理路由啊

```javascript
app.use(session({
  secret: 'WJiol#23123_', //加密的字符串，自己可以随便改
  cookie: {
    path: '/',   //生效的路径 默认为这个
    httpOnly: true,  //是否禁止前端修改cookie 默认为true
    maxAge: 24 * 60 * 60 * 1000 //过期时间，单位毫秒
  },
}))

//下面是
//处理路由
app.use('/', homeRouter);
app.use('/girls',girlsRouter);
```

### 引入redis

redis是一个内存数据库，读写速度很快，可以用来储存session。

1. 在database文件夹下创建一个redis.js。
2. 写代码

```javascript
const redis = require('redis')
const { REDIS_CONF } = require('../confIG/db.js')

// 创建客户端
const redisClient = redis.createClient(REDIS_CONF.port, REDIS_CONF.host)
redisClient.on('error', err => {
    console.error(err)
})

module.exports = redisClient
```

3. 在app.js引入redis

```javascript
const redisStore = require('connect-redis')(session);
```

4. 同样在app.js中，在刚刚那个app.use前面加这个代码，并且在session中加入`store: sessionStore`，也就是说直接把下面这个粘过去就行了。

```javascript
const redisClient = require('./database/redis')
const sessionStore = new redisStore({
  client: redisClient
})
app.use(session({
  secret: 'WJiol#23123_', //加密的字符串，自己可以随便改
  cookie: {
    path: '/',   //生效的路径 默认为这个
    httpOnly: true,  //是否禁止前端修改cookie 默认为true
    maxAge: 24 * 60 * 60 * 1000 //过期时间，单位毫秒
  },
  store: sessionStore
}))
```

5. 开启redis，用终端打开reids的安装目录，输入

```
redis-server.exe
```

之后不要关这个服务器，然后就可以连接redis数据库了。

### 测试session

在home路径下

```javascript
router.get('/session-test', (req, res, next) => {
  //这个session获取的是地址值
    const session = req.session
    if (session.viewNum == null) {
        session.viewNum = 0
    }
    session.viewNum++
    console.log(session===req.session)//true

    res.json({
        viewNum: req.session.viewNum
    })
})
```

可以看到实际上这个session是一直被储存的。

## 代码

1. 建立一个user接口，app.js的父路径为：http://127.0.0.1:3000/users

2. 在data_handle目录下建立一个users.js文件，用于处理用户注册的sql语句

```javascript
//users.js中
const xss = require('xss')
const { exec } = require('../database/mysql')

//登录
const login = (username, password) => {
    let sql = 
    `select username,password
    from users 
    where username = '${username}' and password= '${password}';`

    return exec(sql).then(rows => {
        return rows[0] || {}
    })
}

//注册
const register = (username, password) => {
  let sql = `INSERT INTO users VALUE ('${username}','${password}');`

  return exec(sql)
}


module.exports = {
    login,
    register
}
```

3. 在routes下面建立一个users.js文件，用于处理路由

```javascript
var express = require('express');
var { login,register } = require('../data_handle/users.js')

var router = express.Router();

router.post('/register', function (req, res, next) {
  const { username, password } = req.body
  console.log("注册")
  console.log(username,password)
  const result = register(username, password)
  res.json({
    result
  });
});

module.exports = router;
```

之后用POST请求发几个数据到http://127.0.0.1:3000/users/register，然后发现在sql的客户端查到了数据。

然后再向http://127.0.0.1:3000/users/login发送post请求，注意要加上请求体作为登录信息，然后控制台响应登录成功。

# 日志

## logger

在app.js中，app.use有一个logger的，这个里面其实有一个默认参数，就是下面这个，会不断打印信息。

```javascript
app.use(logger('dev',{
  stream:process.stdout
}));
```

## 记录日志

1. 首先在根目录创建一个logs目录，用于记录日志
2. 里面创建一个access.log文件
3. 在app.use写日志的代码

```javascript
const ENV = process.env.NODE_ENV
if (ENV !== 'production') {
  // 开发环境 / 测试环境
  app.use(logger('dev'));
} else {
  // 线上环境
  const logFileName = path.join(__dirname, 'logs', 'access.log')
  const writeStream = fs.createWriteStream(logFileName, {
    flags: 'a'
  })
  app.use(logger('combined', {
    stream: writeStream
  }));
}
```



# 文件结构

