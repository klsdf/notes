# VUE概述

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

# 基础语法

## 数据绑定 v-bind

v-bind可以动态绑定一个类或者动态绑定样式

### 绑定class

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



### 绑定style

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

## 事件处理 v-on

# 组件化

## 建立组件

```vue
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <title>Document</title>
</head>
<body>
  <div id="app">
    <span>Vue</span>
    <cpn></cpn>
  </div>

  <template id="cpn">
    <div>
      <span>我是组件</span>
    </div>
  </template>


  <script>
    //注册全局组件
    Vue.component('cpn',{
      template:'#cpn',
      //data之所以是函数,因为每个组件都需要自己的值
      //函数return的值刚好是随机分配的内存,每个组件各用各的
      //如果data是一个对象,那么,这个对象会被所有组件共享.
      data(){
        return {};
      },
    })
  
    
    const vue = new Vue({
      el:"#app",
    })
  </script>
</body>
</html>
```



## 子组件通信父组件

```vue
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
    const cvue = {
      template: '#cvue',
      data() {
        return {
          lolis:["傲娇","病娇","天然呆"]
        }
      },
      methods: {
        vueClick(){
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

```vue
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
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

# webpack使用

# vue-cli