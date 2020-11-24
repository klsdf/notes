# 模板语法

## 基本结构

```vue
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        {{ message }}
    </div>
    <script>
        var app = new Vue({
            el: '#app',
            data: {
                message: 'Hello World!'
            }
        })
    </script>
</body>
</html>
```

## moustache语法

将html中的变量用花括号圈起来，在vue里面进行赋值，这种动态数据绑定的方法，就算moustache语法。因为俩个大括号很像胡子？？？？？？我并不理解就是了。

## JavaScript语法支持

在花括号内部，vue支持使用JavaScript语法。

- 四则运算

```vue
<div id="app">
  <div>0{{num+1}}</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      num:720
    }
  })
</script>
```

- 三元表达式

```vue
<div id="app">
  <div>我喜欢{{lolisuki?"萝莉":"幼女"}}</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      lolisuki:true
    }
  })
</script>
```

- 调用方法（以字符串为例）

```vue
<div id="app">
  <!--把字符串变成大写-->
  <div>{{msg.toUpperCase()}}</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      msg:"abcdefg"
    }
  })
</script>
```

# 生命周期

<img src="img/lifecycle.png" alt="Vue 实例生命周期" style="zoom:50%;" />

## 1.beforeCreate

## 2.created

当调用这个函数的对象创建完毕时，立刻回调这个函数。

# 指令

## 文本填充 v-text

v-text会直接替换标签内的全部内容，类似于花括号语法，但是这个是全部替换，那个是指定替换。

```vue
<div id="app">
  <div v-text="msg">test</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      msg:"hello world!!"
    }
  })
</script>
```



## 数据绑定 v-bind

v-bind可以动态绑定一个类或者动态绑定样式。简写时前面用冒号

### 绑定class

#### 绑定单个class

```vue
<!-- head标签内 -->
<style type="text/css">
  .active{
    width: 100px;
    height: 100px;
    background-color: #42B983;
  }
</style>

<!-- /body标签内 -->
<div id="app">
  <div v-bind:class="{ active: isActive }"></div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      isActive: true
    }
  })
</script>
```

#### 绑定多个动态class

```vue
<!-- head标签内 -->
<style type="text/css">
  .active{
    width: 100px;
    height: 100px;
    background-color: #42B983;
  }
  .big-font{
    font-size: larger;
  } 
</style>

<!-- /body标签内 -->
<div id="app">
  <div v-bind:class="[{ active: isActive },fontClass]">绑定class</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      isActive: true,
      fontClass:"big-font"
    }
  })
</script>
```



### 绑定style

```vue
<div id="app">
  <div v-bind:style="{color:colorBind}">绑定style</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      colorBind: "red",
    }
  })
</script>
```

注意!如果绑定的样式含有短线,那么就要替换成对应的驼峰法。

例如：background-color ->backgroundColor



## 双向数据绑定 v-model

### 与checkbox结合

```vue
<p id="app">
	<!-- 单选框 -->
	<input type="checkbox" v-model="isAgree"> 同意协议
	<button v-bind:disabled="!isAgree">下一步</button>
	<br />
	<br />
	<br />
	<!-- 复选框 -->
	<input type="checkbox" v-model="hobby" value="傲娇"> 傲娇
	<input type="checkbox" v-model="hobby" value="天然呆"> 天然呆
	<input type="checkbox" v-model="hobby" value="病娇"> 病娇
	<input type="checkbox" v-model="hobby" value="三无"> 三无
	<br />
	<span>你喜欢的萝莉类型为:{{hobby}}</span>
</p>
<script>
	const vue = new Vue({
		el: "#app",
		data: {
			isAgree: false,
			hobby: [],
		},
	})
</script>
```



### 与radio结合

 v-model其实和value绑定, v-model="sex"就是value为sex属性.

什么意思呢,就是说点击这个input之后,浏览器就会去找v-model绑定的元素是谁,一看发现是sex,然后就会把value的值赋值给sex,最后根据此时sex的值去判断到底选中谁.所以说假如默认赋值为''男"的话,浏览器先开始就会选中value为男的选项.

如果默认sex写的在value里面没有,那么先开始谁都不会选中,点击一次之后,value的值传了进来,之后就一切正常了.

```vue
<p id="app">
	<input type="radio" value="男" v-model="sex">男
	<input type="radio" value="女" v-model="sex"> 女
	<br />
	<span>{{sex}}</span>
</p>
<script>
	const vue = new Vue({
		el: "#app",
		data: {
			sex: '男',
    //sex:'秀吉',
		},
	})
</script>
```

### 修饰符

```vue
  <p id="app">
    <span>lazy可以让数据在失去焦点或者回车才会更新</span>
    <br/>
    <input type="text" v-model.lazy="message" >
    <span>{{message}}</span>
    <br/>
    <span>number可以让数据变为number类型,如果你希望如此</span>
    <br/>
    <input type="text" v-model.number="message2" >
    <span>{{message2}}</span>
    <br/>
    <span>trim可以让数据头尾去除空格</span>
    <br/>
    <input type="text" v-model.trim="message3" >
    <span>{{message3}}</span>
    <br/>
  </p>

    <script>
        const vue=new Vue({
          el:"#app",
          data:{
            message:"123",
            message2:345,
            message3:"",
          },
        })
    </script>
```



## 条件渲染 v-if 和 v-show

## 列表循环 v-for

### 数组循环

对于普通数组而言，v-for就类似于JavaScript中的foreach语法，直接遍历每一项。

```vue
<div id="app">
  <ul>
    <li v-for="item in Language" :key="item">
      {{item}}
    </li>
  </ul>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      Language:["java","c++","python","c#"]
    }
  })
</script>
```

但是对于对象数组而言，直接输出并不是一个好主意。

```vue
<div id="app">
  <ul>
    <li v-for="item in Language" :key="item">
      {{item}}
    </li>
  </ul>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      Language:[{name:"java"},{name:"c++"},{name:"python"},{name:"c#"}]
    }
  })
</script>

<!--结果会变成这样：-->
{ "name": "java" }
{ "name": "c++" }
{ "name": "python" }
{ "name": "c#" }
```

我们可以使用访问属性的方式来遍历

```vue
<li v-for="item in Language" :key="item">
	{{item.name}}
</li>
```

v-for还支持打印数组的下标

```vue
<div id="app">
  <ul>
    <li v-for="(item,index) in Language" :key="index">
      第{{index}}个元素：{{item}}
    </li>
  </ul>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      Language:["java","c++","python","c#"]
    }
  })vue
</script>
```

### 对象循环

类似于数组循环，但是在for的时候，访问的就不是属性了。而是键值对。

```vue
<div id="app">
  <ul>
    <li v-for="(value,key) in loli" :key="key">
      {{key}}为：{{value}}
    </li>
  </ul>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      loli:{
        name:"时雨",
        age:14,
        height:150
      }
    }
  })
</script>
```

### key

key是用来提高列表渲染效率的，必须要选择唯一的那个值。在数组中，index是唯一的，那么就把index设为key。在对象中，键是唯一的，就把key设为key。

## 事件处理 v-on

v-on用于绑定事件处理函数，在JavaScript里面就是onclick,onmousedown之类的，但是vue里面不加on。简写时前面用@

```vue
<body>
  <div id="app">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">反转消息</button>
  </div>
<script>
var app5 = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
```



## v-cloak

VUE渲染的时候，首先会把html页面全显示到网页上，之后再进行替换。这就会导致，如果用户的计算机比较慢，就会直接看到VUE渲染前的页面，体验很差。为了避免这种情况，可以使用v-cloak指令，这个指令首先会把页面隐藏，然后在内存中把页面替换好之后再显示。

使用v-cloak需要先在head里面设置样式才能使用。

```vue
<!--head标签里面-->
<style type="text/css">
  [v-cloak]{
    display: none;
  }
</style>
<!--body标签里面-->
<div id="app">
  <div v-cloak>{{msg}}</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      msg:"hello world!"
    }
  })
</script>
```

## v-once

如果只想让某一个标签只被渲染第一次，也就是说绑定的值就算变化了，这个标签内容也不会改变

```vue
<div id="app">
  <div v-once>{{msg}}</div>
</div>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      msg:"hello world!!!!"
    }
  })
  app.msg="fuck you world!";
</script>
```

可以看到，虽然修改了msg的值，但是v-once作用下，只保留了第一次渲染的值。

## 指令修饰符



# 组件化

## 建立全局组件

1. Vue.component("name",{})方法来注册组件，第一个参数是组件名字，第二个是组件的定义，其中最重要的就是template，它规定了组件的结构内容。
2. 在需要使用的地方直接用组件名的标签就可以了。

```vue
<!DOCTYPE html>
<head>
  <meta charset="UTF-8">
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <title>Document</title>
</head>
<body>
  <div id="app">
    <span>Vue</span>
    <cpn></cpn>
  </div>
  <script>
    //注册全局组件
    //组件名字就是cpn，可以用<cpn></cpn>来使用
    Vue.component('cpn',{
      //模板的内容
      template:'<div><span>我是组件</span></div>',
    })

    const vue = new Vue({
      el:"#app",
    })
  </script>
</body>
</html>
```

## 组件的数据

vue中，除了vue这个大的父组件可以直接用`data:{}`的语法，剩下的组件都必须使用函数的语法。因为组件之间彼此是独立的，而不写函数的话，默认定义的都是全局变量。这就导致所有组件共享数据，不安全。

而写成函数的形式，数据就会被函数封装成局部变量，这样就可以各用各的数据了。

```javascript
data:function() {
	return {
		count: 0
	}
}
```



## 组件抽离

### 1.抽离template

因为template里面是一个字符串，使用可读性很差，还没有代码提示，所以可以把这部分抽离成html代码，提高可读性。html提供了template标签，来定义模板，**要注意，模板里面必须用一个div来包含所有代码**。

```vue
<body>
  <div id="app">
    <span>Vue</span>
    <cpn></cpn>
  </div>
  <template id="tep">
      <div>
        <span>我是组件</span>
      </div>
  </template>
  
  <script>
    Vue.component('cpn', {
      template: '#tep',
    })

    const vue = new Vue({
      el: "#app",
    })
  </script>
</body>
```

### 2.抽离component

现在虽然简单多了，但是还是比较麻烦。每次都要注册vue的**全局组件**，我们可以考虑注册局部组件减少代码量。

1. 首先建立一个对象cpn，把组件的内容写到对象里面
2. 在父组件vue里面声明组件
3. 在html中使用

```vue
<div id="app">
  <span>Vue</span>
  <cpn></cpn>
</div>
<template id="tep">
    <div>
      <span>我是组件</span>
    </div>
</template>

<script>
  const cpn={
    template: '#tep',
  }

  const vue = new Vue({
    el: "#app",
    components:{
      cpn
    }
  })
</script>
```



## 子组件通信父组件

子组件给父组件传递数据，使用的是`this.$emit("对外展示的方法名",数据);`，这样就把子组件的数据对外传递了。那该如何接收呢？在父组件内，用`v-on`来绑定刚才的方法名，然后调用父组件的方法。此时父组件的参数就是子组件的数据了。

```vue
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <title>Document</title>
</head>

<body>
  <div id="app">
    <span>我是父组件Vue</span>
    <cvue v-on:vue-click="showChildMessage"></cvue>
  </div>

  <template id="cvue">
    <div>
      <button v-on:click="vueClick">我是子组件</button>
    </div>
  </template>


  <script>
    //子组件
    const cvue = {
      template: '#cvue',
      data() {
        return {
          lolis:["傲娇","病娇","天然呆"]
        }
      },
      methods: {
        vueClick(){
          //用$emit来暴露数据和接收数据的方法
          this.$emit("vue-click",this.lolis);
        }
      },
    }


    const vue = new Vue({
      el: "#app",
      components: {
        cvue,
      },
      methods: {
        //父组件的参数就算子组件暴露的数据
        showChildMessage(lolis){
          alert(lolis);
        }
      },
    })
  </script>
</body>

</html>
```

## 父组件通信子组件

父组件不能直接把数据给子组件，而是通过父组件给子组件的prop属性传递数据来间接实现。那首先就算给子组件建立prop属性，之后用`v-bind`把子组件的prop数据和父组件绑定。

```vue
<!DOCTYPE html>

<head>
  <meta charset="UTF-8">
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <title>Document</title>
</head>

<body>
  <div id="app">
    <span>我是父组件Vue</span>
    <cvue v-bind:cmessage="message"></cvue>
  </div>

  <template id="cvue">
    <div>
      <span>我是子组件{{cmessage}}</span>
    </div>
  </template>


  <script>
    const cvue = {
      template: '#cvue',
      props: {
        cmessage:{
          type:String,
          default:"默认值",
        }
      },
    }


    const vue = new Vue({
      el: "#app",
      data: {
        message: "hello world",
      },
      components: {
        cvue,
      }
    })
  </script>
</body>

</html>
```

## 插槽

### 普通插槽

对于template的模板来说，如果一次性写死，有可能造成代码难以复用，所以把这些模板写的越抽象，日后功能就会越强大。template就提供了这样的功能，也就是插槽。

使用方法其实非常简单，就是在template里面加一个slot标签，表示这个可以被替换。

我这个例子里面写了一个span标签，就表示默认情况下插入这个萝莉span，如果在html中你插入了其他的数据，那么就会替换我原来的值。这个`<span>萝莉</span>`，就是默认值。

```vue
<body>
  <div id="app">
    <cvue></cvue>
    <cvue><span>幼女</span></cvue>
  </div>

  <template id="cvue">
    <div>
      <span>
        我喜欢：
        <slot><span>萝莉</span></slot>
      </span>
    </div>
  </template>


  <script>
    const cvue = {
      template: '#cvue',
    }


    const vue = new Vue({
      el: "#app",
      components: {
        cvue,
      }
    })
  </script>
</body>
```

### 具名插槽

在开发中，一个模板里面其实可能出现多个插槽，如果还是像刚才一样直接插入，可能会导致二义性，也就是分不清到底是给谁插的。为了避免这种情况，vue提供了具名插槽。

具名插槽使用起来也很简单，首先给slot起名字，使用的时候用slot属性去找对应的name就可以了。 

```vue
<body>
  <div id="app">
    <cvue>
      <span slot="first">身娇</span>
      <span slot="second">体柔</span>
      <span slot="third">易推倒</span>
    </cvue>
  </div>

  <template id="cvue">
    <div>
        <div>萝莉有三好</div>
        1.<slot name="first"></slot>
        2.<slot name="second"></slot>
        3.<slot name="third"></slot>
    </div>
  </template>


  <script>
    const cvue = {
      template: '#cvue',
    }
    const vue = new Vue({
      el: "#app",
      components: {
        cvue,
      }
    })
  </script>
</body>
```



# webpack

webpack是一个JavaScript的静态打包工具，webpack会把你写的代码进行打包，把ES6，commonJS等浏览器可能不支持的语法转化为ES5，确保所有浏览器都支持。非常非常方便，再也不用考虑兼容。

webpack是我们面向正式项目开发的第一步。

如果下面的看不懂，建议先去看看node的模块化。

## 安装

首先得要有node的环境，没有的去看我node的教程。然后安装 webpack和webpack-cli

先介绍一下安装类型

```shell
npm install webpack -g  //全局安装
npm install webpack --save-dev // 项目内局部安装
//还可以指定版本号
npm install webpack@3.6.0 --save-dev
```

挑一个进行安装，我的如下

```shell
npm install webpack webpack-cli --save-dev
```



## 打包与运行

首先初始化环境，在项目根目录运行

```shell
npm init -y
```

之后打包，默认采用最新的版本命令，如果是4.0之前的webpack版本，请去掉-o

```powershell
webpack 要打包文件的路径 -o 目标路径\文件名字
//我的代码如下
webpack  .\src\main.js -o .\dist\bundle.js
```

这时候可能会出现错误：

```shell
webpack : File C:\Users\17966\AppData\Roaming\npm\webpack.ps1 cannot be loaded because running scripts is disabled on 
this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
```

这是因为没有开启权限，用powershell开启一下权限就可以了。

在powershell里面输入：之后A就可以了。

```powershell
set-ExecutionPolicy RemoteSigned
```

还可以再输入下面的指令确认

```powershell
get-ExecutionPolicy
```

运行就很简单了，建一个index.html，引入打包后的js文件

```html
<!DOCTYPE html>
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <script src="./dist/bundle.js"></script>
</head>
<body>
</body>
</html>
```



## 配置

### webpack.config.js

这个是需要我们自己创建的一个配置文件。如果每次都要用刚才那一大串命令来打包，未免太麻烦了，也没有一个更加简单的方法呢？仅仅输入webpack就可以执行上述的命令。当然可以了，这时候我们只需要把命令都配置进webpack.config.js里面，就可以用webpack来简化命令了。

首先需要指定一个入口的main.js文件，这个是用的相对路径，比较好处理。之后还有一个输出打包文件的路径，这个需要绝对路径，我们可以用node里面的path模块来进行绝对路径的拼接。

```javascript
var path = require("path");
// npm init
//配置之后自动打包
module.exports = {
  entry: "./src/main.js",
  output: {
    //打包路径
    path: path.resolve(__dirname, "dist"),
    //文件名
    filename: "bundle.js",
  }
}
```

### package.json

其实在实际开发中，我们都是用`npm run build`来打包。那如何把这个npm的命令和webpack的命令结合起来呢？

首先我们要知道`npm run xxx`是什么意思，其实很简单，如果在命令行输入这个命令，那么编译器就会去寻找package.json文件中的`  "scripts"`键，也就是属性名，然后去寻找里面的xxx命令并运行。也就是说，如果想要执行`npm run build`，其实就是在package.json中的script里面配置一个build属性就行了。

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
```

之后就可以用`npm run build `命令执行打包了。

```shell
npm run build
```

配置这个好处在于，这个命令会调用局部的webpack指令，也就是位于，而不是全局的，可以防止全局版本和局部版本不兼容的bug。

## 文件结构

我们既然开始模块化开发了，那么就要有一套严格的代码标准。以确保可读性和重用。

- 根目录
  - dist：打包好的文件，这个是放到服务器上的最终代码
  
  - src：源代码，你写的都在这里
    
    - CSS文件夹：存的样式文件
    
    - JS文件夹：存的各种js代码
    - VUE文件夹：存放各种vue文件
    
    - main.js：入口js文件，链接了各种js文件，这种入口文件就单独拿出来，不要放到文件夹里面。
    
  - index.html：主html文件，核心文件。



## loader

刚才webpack的命令只能打包js和json，如果只是这样就太鸡肋了。所以肯定还有别的技术来打包其他的文件。这种技术就是loader。

### css loader

css可以来打包css文件，需要安装css-loader和style-loader，css-loader负责加载样式，style-loader负责将样式加入DOM中，缺一不可。

```shell
npm install  css-loader style-loader --save-dev
```

之后需要配置webpack.config.js

```javascript
module.exports = {
  entry: "./src/main.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ["style-loader","css-loader"]
      }
    ]
  }
}
```

注意use里面的顺序不能更改！！因为loader是从右往左加载的，所以要把css-loader写在右边。

使用时直接在main.js里面require就行了。

### vue loader

这个在后面会说到，看到后面的时候可以回到前面来看，或者复习用。

首先是安装：

vue-loader用于加载vue文件，vue-template-compiler用于编译vue文件。

```shell
npm install vue-loader vue-template-compiler --save-dev
```

然后是配置：

```javascript
{
  test: /\.vue$/,
  loader:"vue-loader",
}
```

然后你会发现还是报错，这是因为Vue Loader v15 现在需要配合一个 webpack 插件才能正确使用，所以还要配置下面的部分：

```javascript
// webpack.config.js
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
  // ...
  plugins: [
    new VueLoaderPlugin()
  ]
}
```



## vue与webpack

### 安装与配置

这个是运行依赖的，因为项目写好后运行也是需要用vue支持的。而webpack仅仅是打包时要用到。

```shell
npm install vue --save
```

之后在webpack.config.js中添加，因为vue版本很多，默认的版本是仅仅运行时依赖，这就会导致无法使用template，所以要修改默认版本。

```javascript
  resolve:{
    alias:{
      "vue$":"vue/dist/vue.esm.js",
    }
  },
```

之后切记，script要放在vue挂载标签的下面！！！！，因为页面加载的时候是安装顺序执行的，如果像以前一样放在head里面，就导致渲染msg的时候，msg还没有加载出来。跟之前学DOM一样的原理。

```html
<!--index.html-->
<body>
  <div id="app">
    {{msg}}
  </div>
  <script src="./dist//bundle.js"></script>
</body>
```

```javascript
//main.js
import Vue from 'vue'

var app = new Vue({
  el: '#app',
  data: {
    msg: 'Hello Vue!'
  }
})

```

### 组件抽离

之前我们已经学过一次组建抽离了，但是这次我们是基于webpack进行的更加抽象的抽离。

#### 抽离index.html

目前我们的index.html里面还是有实际的结构和数据，`<div id="app">{{msg}}</div>`，这个对于模板化开发来说实在是太不像样子，所以我们首先要把主html的内容抽出来。

vue提供了这样的方法，vue也是一个组件，是所有组件的父组件。所以vue也会有template属性，**这个template会在编译时直接替换el挂载点所在标签的全部内容**。也就是说，vue内定义的template会直接替换`<div id="app">{{msg}}</div>`。

这样一来，我们就可以直接把index.html中大大简化，也就是说只保留`<div id="app"></div>`，剩下的全部在main.js实现

```html
<!--index.html-->
<body>
  <div id="app"></div>
  <script src="./dist//bundle.js"></script>
</body>
```

```javascript
//main.js
import Vue from 'vue'

var app = new Vue({
  el: '#app',
  template: ` 
<div id="app">
  {{msg}}
</div>`,
  data: {
    msg: 'Hello Vue!'
  }
})
```

#### 抽离main.js

现在index.html简单了，但是main.js却复杂了，但是我们之前已经学过了如何抽离template，所以其实main.js非常好模板化。

1. 把vue中的template抽成组件
2. 在vue的components中注册
3. 在template中直接把注册好的组件写上，替换挂载点的内容。

```javascript
import Vue from 'vue'
const App ={
  template: ` 
  <div id="app">
    {{msg}}
  </div>`,
  data() {
    return {
      msg: 'Hello Vue!'
    }
  },
}
var app = new Vue({
  el: '#app',
  template: `<App/>`,
  components:{
    App
  }
})

```

#### 抽离到.vue文件

这时候就到了另一个重点了，我们之前抽离template是直接放到html里面的，现在我这个main.js是一个完完全全的js文件，抽不出来，该怎么办呢？？？其实很容易想到，抽到另一个html文件不就可以了？虽然可以，但是这样就让文件彼此逻辑太混乱了，我这个template,data,style等文件明显就是一体的，强行抽开不太合适，怎么办呢？vue的设计大佬们引出了一个vue文件，用于集合上述的格式。

在VUE文件夹里面建立一个App.vue文件，然后把刚才那个App移植到APP.vue文件里面

```vue
<!-- App.vue -->
<template>
	<div>
		{{msg}}
	</div>
</template>

<script>
	export default {
		name: "App",
		data() {
			return {
				msg: "hello VUE！",
			}
		},
	};
</script>

<style>
</style>

```

然后main.js里面就只用引入App就可以了

```javascript
//main.js
import Vue from 'vue'
import App from "./VUE/App.vue"
var app = new Vue({
  el: '#app',
  template: `<App/>`,
  components:{
    App
  }
})
```

## 插件

插件是用于拓展webpack功能的，在webpack.config.js中的plugin中使用，一般来说按需添加。

这里以一个版权插件为例：

```javascript
// webpack.config.js
const webpack = require("webpack")

module.exports = {
  // ...
   plugins: [
    new webpack.BannerPlugin("版权归本人所有")
  ]
}
```

之后可以发现在bundle.js里面多了一个注释，里面写着你的版权信息。

# vue-cli

CLI是Command-Line Interface，翻译为命令行界面,但是俗称脚手架。CLI可以快速搭建Vue开发环境以及对应的webpack配置。

## 安装

首先需要node和webpack环境。之后全局安装。

```shell
npm install -g @vue/cli
```

最后可以用大写-V查看版本号。

```shell
vue -V
```

但是我们这个安装的默认最高版本，所以导致旧版的项目可能不兼容，所以还要安装一下旧版本的模板。

```shell
npm install @vue/cli -init -g
```

## 项目创建与运行

不同版本的创建命令不一样，需要特别注意：

```shell
//cli2
vue init webpack 项目名

//cli3及以上
vue create 项目名
```

以cli3为例，输入指令以后会出现下面的提示

```shell
? Please pick a preset: (Use arrow keys)
> Default ([Vue 2] babel, eslint)
  Default (Vue 3 Preview) ([Vue 3] babel, eslint) 
  Manually select features
```

方向键选择`Manually select features`，然后回车。接下来出现这个。

注释是我加的。

```shell
? Please pick a preset: Manually select features
? Check the features needed for your project: (Press <space> to select, <a> to toggle all, <i> to invert selection)
 (*) Choose Vue version     //自己选vue版本
 (*) Babel									//es6转es5
>( ) TypeScript           //支持typescript
 ( ) Progressive Web App (PWA) Support   //先进网络应用支持
 ( ) Router        //vue静态路由
 ( ) Vuex          //vuex
 ( ) CSS Pre-processors    //css预处理器
 (*) Linter / Formatter  //ESlint严格语法标准，别选
 ( ) Unit Testing				//单元测试
 ( ) E2E Testing				//端到端测试
```

之后出现这个，选第一个

```shell
? Where do you prefer placing config for Babel, ESLint, etc.? (Use arrow keys)    
> In dedicated config files   //独立配置文件
  In package.json    //全放到package.json
```

最后，是否把刚才的设置保存下来？目前建议选N。

```shell
Save this as a preset for future projects? (y/N)
```

如果不小心保存了，在哪里删呢？

C:\Users\用户名   里面有一个.vuerc文件，里面的presets就保存了你的配置，删掉presets里面的内容就行了。

最后使用serve运行

```shell
npm run serve
```

想要打包项目，使用

```shell
 npm run build
```

具体在package.json中都有写到。

## 目录结构

- node_modules：通过npm安装的一大推包
- public：公用的文件，最后直接原封不动封进dist文件夹
- src：源代码
- .browserslistrc：浏览器配置
- .gitignore：git的配置，选择上传git时忽略哪些文件
- babel.config.js：不懂
- package-lock.json：记录着各个插件的版本信息
- package.json：主要配置，以后经常要写
- README.md：记录版权信息，使用方法，作者吐槽什么什么的，没有固定用法。

## vue ui 

cli3以上版本超级无敌牛逼的东西，也就是可视化配置，再也不需要去手动改json了，直接可视化全自动操作，我爱死这个东西了。

开启方法很简单：

```shell
vue ui
```

## vue-router

这个router并不是路由器，而是指前端的静态路由。

### 安装

```shell
npm install vue-router --save
```

或者直接在vue ui安装，或者一开始安装cli的时候就把router选上。

建议去vue ui里面安装，vue-router属于插件，直接去插件里面安装。

### 路由映射的配置

在router文件夹下的index.js文件配置，这个是注册路由的。

```javascript
import Home from '../views/Home.vue'
const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  }
]
```

之后在App.vue里面写上注册过路由的组件，不过直接用肯定没有效果啦，vue提供了一个``<router-link>`标签，便于实现路由跳转，这个标签里面有一个to属性，写要转去的url。最后一定要加上`<router-view/>`，以便显示路由的内容。

```vue
<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <router-view/>
</template>
```

### 代码控制路由跳转

` router-link`是vue自己封装的组件，但是我们有时候并不想用这种固定的方式来跳转路由，这时候我们就可以手动用JS来跳转。比如可以写一个v-on来绑定一个响应函数，里面写上

```javascript
itemClick(){
  this.$router.push('需要跳转的url')
}
```

这个方法会让你的浏览器加载下一个url，也就是说浏览记录里面可能会有一大堆无用的记录，建议换成下面的。

```javascript
itemClick(){
	this.$router.replace('需要跳转的url')
}
```

如果是新版的cli，点两次可能会报错，这是因为新版的router重写了push方法，导致重复跳转时会报错。这时只需要在router下的index.js里面加上这个代码，直接粘过去就行。

```javascript
//重写push和replace方法，防止路由重复跳转报错。
import VueRouter from "vue-router";

//push
const VueRouterPush = VueRouter.prototype.push
VueRouter.prototype.push = function push (to) {
    return VueRouterPush.call(this, to).catch(err => err)
}

//replace
const VueRouterReplace = VueRouter.prototype.replace
VueRouter.prototype.replace = function replace (to) {
  return VueRouterReplace.call(this, to).catch(err => err)
}
```



### 路由重定向

一般来说，我们打开网站，都是默认在首页。这个就是靠路由默认跳转到首页来实现的，如何做到这个效果呢？靠的就是路由重定向。也就是说如果一旦进入某个url，立刻跳转到指定的url。有点像钓鱼网站。

path指的是用户输入的url，redirect就是默认跳转的url。

```javascript
{
  path:'/',
  redirect:'/home'
},
```

### router-link标签的属性

vue-router中引入了router-link标签，用于用户点击来实现页面跳转，这个标签功能非常强大，有很多重要的属性。

- to：用于标记跳转的页面url
- tag：一般情况下，router-link会被渲染成a标签，但是这个tag可以指定最终渲染成的标签  tag='div'
- replace：写了这个，跳转页面的时候就会用replace方法，而不是push，可以避免不必要的历史记录。

### 动态路由

所谓动态路由就是在网页的url后面，动态地添加所需的内容。比如说商品网的url为 /shop/，接下来需求是每点一个商品，后面的url自动拼接商品名。比如 /shop/cat/     /shop/pen/  这样子可以标记每一个组件的url。但是商品这么多，又不可能把所有的url提前写好，并且一旦商品替换，url又得重写。为了避免这个问题，我们可以使用动态路由技术。

第一步，创建一个商品组件，并且注册路由。不多说了。

第二步，修改路由配置，给shop后面加一个`:id`，这个id就是一个变量，表示往url后面拼接的那个变量。

```javascript
{
  path: '/shop/:id',
  name:'Shop',
  component:()=>import('../views/Shop.vue')
}
```

第三步，来给这个id变量绑定值吧。我们这个shop组件是在App组件中引用的，也是在这个里面进行路由跳转的，所以当然也是在这个里面进行id的绑定。核心步骤只有一个，就是让data返回一个商品id，然后用v-bind后面拼接上这个变量。这样点看网页，url后面就会自动拼接上猫娘了。

```vue
//App.vue
<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>|
    <router-link v-bind:to="'/shop/'+goodsId">Shop</router-link>
  </div>
  <router-view/>
</template>

<script>
export default {
  name:'App',
  data() {
    return {
      goodsId:"猫娘"
    }
  },
}
</script>
```

第四步，如果需要在商品页使用这个goodsId的话，那么就会有第四步。首先，自定义一个计算属性，return  当前活跃路由的变量值，这个id并不是本身带的，而是刚刚在路由配置里面咱自己定义的。拿到的这个id，其实就是goodsId:"猫娘"。App.vue先把数据传给了url，之后商品页又从url那里拿到了这个值。之后就可以愉快地使用了。

```vue
<template>
  <div class="shop">
    <span>我是商品页</span>
    <span>当前浏览的商品是{{goodsId}}</span>
  </div>
</template>

<script>
export default {
  name: 'Home',
  computed: {
    goodsId(){
      return this.$route.params.id
    }
  },
}
</script>
```

### 路由懒加载

当打包构建应用时，Javascript包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。

虽然早期路由懒加载非常复杂，但是新版本的写法已经很简单了。其实`component: () => import()`就是路由懒加载，而Home也是懒加载，也就是说只要是import进来的数据就是懒加载。

```javascript
import Home from '../views/Home.vue'

const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  },
  {
    path: '/shop/:id',
    name:'Shop',
    component:()=>import('../views/Shop.vue')
  }
]
```

### 子路由

这个其实就是子页面，首页下可能有多个子页面，比如说新闻，推荐之类的。单独再开一个页面肯定不合适，所以可以在首页创建子页面。比如 /Home要和上面那个动态路由区分，上面那个是重开了一个新页面。

首先，建立子组件，不多说了。

之后，配置路由，直接在home中写一个children就可以了，注意，子组件的path不需要写/，编译器会自动帮你拼接斜线的。因为以“/”开头的嵌套路径会被当作根路径，所以子路由上不用加“/”。

```javascript
  {
    path: '/home',
    component: Home,
    children: [
      {
        path: 'news',
        component: () => import('../components/homeNews.vue')
      },
      {
        path: 'recommend',
        component: () => import('../components/homeRec.vue')
      },
    ]
  },
```

之后，跟之前一样，在home页，把这两个router-link写上，以便访问。最后别忘了router-view

```vue
<template>
  <div class="home">
    <div>我是首页</div>
    <router-link to="/home/news">新闻</router-link>|
    <router-link to="/home/recommend">推荐</router-link>
    <router-view></router-view>
  </div>
</template>
```

最后如果想要重定向首页到某个具体组件，可以这么修改。

```javascript
{
  path: '/',
  redirect: '/home/news'
},
```



我发现如果有多层子路由，那么不能一下子跳转到多层子路由。比如说我现在有了多层子路由，但是从Computer这个页面只能跳转到FrontEnd，就算写了HTML的页面，爷跳不过去。非常神秘，难以理解。

```javascript
const routes = [
	// 默认路由重定向
	{
		path: '',
		redirect: '/Home',
	},
	{
		path: '/Home',
		name: 'Home',
		component: () => import('views/Home/Home.vue')
	},
	{
		path: '/Computer',
		name: 'Computer',
		component: () => import('views/Computer/Computer.vue'),
		children:[
			{
				path: 'FrontEnd',
				name: 'FrontEnd',
				component: () => import('views/Computer/FrontEnd/FrontEnd.vue'),
				children:[
					{
							path: 'HTML',
							name: 'HTML',
							component: () => import('views/Computer/FrontEnd/HTML/HTML.vue')
					},
					{
						path: 'CSS',
						name: 'CSS',
						component: () => import('views/Computer/FrontEnd/CSS/CSS.vue')
				},
				]
      },
		]
```

![image-20201023230412696](img/image-20201023230412696.png)

可以看到，无法进行多层跳转，最多跳一层。

## vuex

vuex是一个状态管理工具，我们的项目开发到后期，组件之间相互调用形成的组件树非常复杂，而有一些全局的变量，在组件相互调用时就会非常难以管理。为了管理这些组件的公有变量，我们就需要vuex来统一管理。

vuex是一个单例模式，这是为了更加清除地管理，如果允许多个store，那么数据就太混乱了，日后管理维护就是噩梦。

### 安装

可以用

```shell
npm install vuex --save
```

或者用万能的vue ui 来可视化安装。之后会多出来一个store文件夹。

### 结构

```javascript
export default createStore({
  state: {
    //存放数据
  },
  mutations: {
    //存放方法
  },
  actions: {
  },
  modules: {
  }
})
```

### 使用方法

- 通过`this.$store.state.属性`的方式来访问数据
- 通过`this.$store.commit('mutation中的方法')`来调用mutation中的方法

## axios

### 安装

```shell
 npm install axios --save
```

### get请求

```javascript
import axios from 'axios'

axios({
  //请求的服务器url
  url:"http://123.207.32.32:8000/home/multidata",
  //请求类型
  method:'GET',
  //针对get请求的参数拼接
  params:{
    type:'pop',
    page:1
  }
}).then(resualt=>{
  console.log(resualt)
})
```

### post请求

```javascript
import axios from 'axios'

axios({
  //请求的服务器url
  url:"http://123.207.32.32:8000/home/multidata",
  //请求类型
  method:'POST',
  //针对get请求的参数拼接
  data:{
    type:'pop',
    page:1
  }
}).then(resualt=>{
  console.log(resualt)
})
```



### axios全局配置

一些经常使用的变量，可以抽出来全局配置。这些变量都是axios提前定义好的，可以直接用defaults来引用。

```javascript
//主机url
axios.defaults.baseURL = "http://123.207.32.32:8000"
//延时时间
axios.defaults.timeout = 3000
axios({
  url: "/home/multidata",
  method: 'GET',
  params: {
    //针对get请求的参数拼接
    type: 'pop',
    page: 1
  }
}).then(resualt => {
  console.log(resualt)
})
```

### 创建axios实例对象

我们刚才所使用的都是一个axios对象，同样的，刚才那些使用方法也都是在一个服务器上的。如果后端的服务器采用分布式设计，那么不同服务器就有不同的url，设置的baseURL就不能满足所有人需求。

此时，我们可以直接创建多个axios的实例对象，每一个都拥有自己的baseURL和timeout等属性。

```javascript
import axios from 'axios'
//创建一个axios的实例对象
const axiosInstance=axios.create({
  baseURL:"http://123.207.32.32:8000",
  timeout:3000
})
//直接用实例对象发送请求
axiosInstance({
  url: "/home/multidata",
  method: 'GET',
  params: {
    type: 'pop',
    page: 1
  }
}).then(resualt => {
  console.log(resualt)
})
```

这样子，对每个服务器都可以创建一个独有的axios对象，进行特别配置。

### Promise封装

我们可以对网络请求进行一个封装，把请求的方法封装进一个js文件，这个文件里面再封装axios的各种方法和配置。

```javascript
import axios from 'axios'

export default request(config){
  return new Promise((resolve,reject)=>{
    const instance = axios.create({
      baseURL:"http://123.207.32.32:8000",
      timeout:5000
    })
    instance(config)
    .then(res=>{
      resolve(res)
    })
    .catch(err=>{
      reject(err)
    })
  })
}
```

但是实际上，`axios.create`的结果本身就自带一个promise，所以我们可以直接用就行了。

```javascript
import axios from 'axios'

export default request(config){
    const instance = axios.create({
      baseURL:"http://123.207.32.32:8000",
      timeout:5000
    })
    return instance(config)
}
```

### 拦截器

这个东西可以把服务器那里请求过来的数据做一个拦截，进行修改或者什么神秘操作。

1. 修改config中不符合服务器规范的配置
2. 在发送网络请求时，在页面显示加载图片
3. 某些网络请求（比如登录），要求用户输入一些特殊信息，

```javascript
import axios from 'axios'

export default request(config){
    const instance = axios.create({
      baseURL:"http://123.207.32.32:8000",
      timeout:5000
    })


    //发送request的拦截
    instance.interceptors.request.use(request=>{
      console.log("已经拦截到用户请求")
      //把拦截掉的请求释放
      return request
    },error=>{
      //当用户请求发不出去时调用，比如断网
      console.log("用户请求发送失败")
    })

    //服务器响应结果的拦截
    instance.interceptors.response.use(response=>{
      console.log("已经拦截到服务器响应")
      //把拦截掉的响应释放
      return response.data
    },error=>{
      //当服务器响应失败时执行，比如404
      console.log("用户请求发送失败")
    })

    return instance(config)
}
```

