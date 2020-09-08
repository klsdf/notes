# 基础知识

本文采用了最新的es6语法,可以放心食用.

## 专业术语

为了防止在文中反复解释一些术语,我将一些常用术语的解释放在了这里.这意味着你并不需要直接看这里.等之后遇到了这些术语再翻上来看才是正道.

### ES6

### 字面量

字面量就是代码意义上的常量,说白了就是可以放到赋值号右边的都可以叫字面量.这样子这个赋值表达式的值就如字面上一样,你赋值号右边写的是啥,值就是啥,非常容易理解.

**注意,我下面代码中赋值语句的右边是字面量,我写这个语句只是方便理解,别理解错了.**

```javascript
var 字符串字面量 = "hello world!";
var 数值字面量 = 996;
var 数组字面量 = ["java","c++","JavaScript"];
var 函数字面量 = function(){}
var 对象字面量 = {}
```

### 函数与方法

理论上对象的函数就叫做方法,但是JavaScript是纯面向对象的语言,万物皆对象.所以函数和方法并没有C++那种半面向对象语言那种严格.一般来讲,window对象的方法叫做函数,其他对象的函数叫做方法,不过也没有那么较真就是了.

## 关于结尾的分号

JavaScript并没有强制要求你加上分号,也没有要求一定不加,一般情况下看自己喜好就行.

不过只有这么两种情况下必须加分号:

## 双引号与单引号

JavaScript不区分单引号和双引号,字符串可以随意用这两种引号,不像其他语言严格取分大小写

## Hello World

浏览器环境下,直接打开浏览器,F12找到console就能看到.

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript">
			console.log("Hello World");
		</script>
	</head>
	<body>
	</body>
</html>

```

node环境下,用node命令执行语句.

```javascript
console.log("Hello World");
```



# 值类型

# 引用类型之字符串

## 定义与使用

```javascript
//用字面量创建
var dream ="愿天下没有996!";
```



## 字符串常用方法

es6 新增字符串方法

- includes()

- startWith()

  ```javascript
  //字符串开头字母之后的字符串是否为h
  str.startWith("h");
  //字符串开头第2个字母之后的字符串是否为ello
  str.startWith("ello",1);
  ```

  

- endWith()

## 模板字符串

模板字符串是超级无敌强化之后的字符串,用**间隔符**(ESC下面那个符号)来引用.

下面简述它的两个主要功能

1. 可以在字符串内直接使用变量,并计算
2. 可以在字符串内保留回车,不用自己拼接回车了.

当一个字符串拼接的过长时,原来那种+号的写法过于繁琐,所以可以使用模板字符串,直接把变量放在里面

```javascript
//注意,return中的是间隔符,并不是引号.
function KillerQueen(name,age){
	return `我叫${name},今年${age}岁`
}
console.log(KillerQueen("吉良吉影",33));
```

不仅仅是这样,模板字符串里面的变量也可以进行运算,并且保留回车.

```javascript
function Real_GDP_per_capita(money){
	return `
		赵家有钱${money}万,隔壁9个穷光蛋;
		平均起来算一算,各个都是赵${money/(9+1)}万`;
}
console.log(Real_GDP_per_capita(1000));
```



# 数组

## 数组常用方法

1. concat() 可以拼接两个数组

   ```javascript
   var loli1 = ["雷姆","伊莉雅","波莱特","巧克力"];
   var loli2 = ["86","香子兰","牛顿"];
   console.log(loli1.concat(loli2));
   ```

   

# 函数

## 简介

​	JavaScript的函数就是对象,万物皆对象.但是JavaScript是弱数据类型的,所以在使用函数的时候和别的强数据类型语言还是有差别.

就比如说,函数不用写返回值类型,没有返回值也不用 `return void;` ,并且定义时需要显式定义.

## 定义与使用

函数有两种定义方法(暂时不考虑箭头函数),没有什么好说的,记住就行了.

```javascript
function add(a, b) {
	return a + b;          
}
//下面这个是字面量创建
var add = function(a,b){
  return a + b;      
}
```

使用也没有什么好说的,跟其他语言一样

```javascript
add(a,b);
```



## 立即执行函数

​	把一个匿名函数前后都用小括号括起来就变成了立即执行函数,这种函数只能用一次,一旦程序运行到这里立刻执行.

因为没有名字,之后无法被其他程序调用.

```javascript
(function(){
  document.write("我是匿名函数")
})(); 
```



## 箭头函数

这个东西看着复杂,实际上就是一个简化版匿名函数,

我们可以用匿名函数来参考着看.

```javascript 
var fun1 = function (id){
	console.log("匿名函数"+id);
}
var fun2 = (id) => {
	console.log("箭头函数"+id);
}
fun1(0);
fun2(1);
```

若函数,只有一个参数,可以省略小括号,但是没有参数的话,必须加一个空括号().

并且函数只有一行代码的话,可以省略大括号,经典操作了.

```javascript
var fun1 = function (id){
	console.log("匿名函数"+id);
}
var fun2 = id => console.log("箭头函数");
fun1();
fun2();
```

是不是一下子就简化很多了.但是这个还是有一个需要说明的地方.

注意!**如果没有大括号,那么编译器默认会给前面加上return,返回该语句.**

```javascript
var fun2 = () => "0"+721;
console.log( fun2());
```

最后结果返回0721.(柚子厨震怒)

## rest参数

当函数不确定具体有多少参数时,可以使用rest参数,来统一获取剩下所有参数.

我们用**三个点**代表rest参数 ... 

```javascript
function Lolis(...lolis){
	for(let girl of lolis)
		console.log(girl);
}
Lolis("雷姆","伊莉雅","波莱特","巧克力");
```

可以发现我在console的时候,用了for of语法,这就说明,其实rest参数会把传进来的所有参数封装成数组,可以用数组的方法操作rest参数.

## 高阶函数

```javascript
const nums = [2, 4, 8, 16, 32, 64, 128, 256, 512, 1024];
//filter用来过滤想要的数据
//filter函数会调用一个回调函数
//回调函数的参数n会遍历nums数组的元素
//回调函数必须返回一个boolean值,
//若为true则把数据压入新数组,false则过滤掉
var newNums = nums.filter(
  function (item) {
    if (item > 100)
      return true;
  }
);
console.log("newNums:"+newNums);

//map用来对原数据进行一次映射
//对数组进行一次映射,遍历数组每一项,把数据存入n中,
//return的值存入新的数组
var newNums2 = newNums.map(
  function (item) {
    return item * 10
  }
);
console.log("newNums2:"+newNums2);

//用于集合中的所有数据,可以进行如全部加一遍的操作
//reduce一共传参两个,第一个是回调函数,第二个是给oldValue初始化的值
//回调函数中,oldValue除第一次外,每次值被赋值为函数return的值
//item依旧遍历之前的数组
var newNums3 = newNums2.reduce(function (oldValue, item) {
  return oldValue + item;
}, 0);
console.log("newNums3:"+newNums3);

var totle = nums.filter(function (item) {
  if (item > 100)
    return true;
}
                       ).map(function (item) {
  return item * 10;
}
                            ).reduce(function (oldValue, item) {
  return oldValue+item;
}, 0);
console.log("totle:"+totle);
//箭头函数写法
var totle2=nums.filter(item=>item>100).map(item=>item*10).reduce((pre,item)=>item+pre);
console.log("totle2:"+totle2);
```



# 引用类型之对象

# 类

## 类的创建

### ES5



### ES6

类可以来创建对象,因为ES6真的很香,跟java他们用法差不多,现在你就能发现ES6有多香了.S5学起来简直难受的一批,浑身不舒服.

```javascript
class Loli {
    constructor(age) {
        this.age = age;
    }
	gulu_gulu()
	{
		console.log("咕噜咕噜~~~");
	}
	showAge(){
		console.log(`人家今年${this.age}岁`);
	}
  //静态方法
	static ne()
	{
		console.log("呐呐呐呐呐呐呐呐呐呐呐呐呐呐呐呐");
	}
}
var 巧克力 = new Loli(14);
巧克力.gulu_gulu();
巧克力.showAge();
Loli.ne();
```

可以看到,程序正常运行:

![image-20200831233256840](img\image-20200831233256840.png)

## 类的继承

用extends表示继承哪个类,之后用super来指定继承的属性,默认继承全部的方法.

```javascript
class 天然呆萝莉 extends Loli {
	constructor(age,name) {
		//用super来直接继承属性
	  super(age);
		this.name=name;
	}
	//方法默认全部继承过来,无论是普通方法,还是静态方法.
	showInfo(){
		console.log(`嘟嘟噜~~,${this.name}です,今年${this.age}岁`)
	}
}
var 椎名真由理 = new 天然呆萝莉(14,"椎名真由理");
椎名真由理.showInfo();
椎名真由理.gulu_gulu();
天然呆萝莉.ne();
```
可以看到程序正常运行:

![image-20200831233416082](img\image-20200831233416082.png)

# this

精通this是你从JS萌新变成JS巨佬的必经之路,但是想熟练掌握这个东西,并不是一件轻松的工作..







# JSON

# BOM和DOM

# 2020/8/31