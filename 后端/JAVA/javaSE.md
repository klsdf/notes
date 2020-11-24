
# 基础知识

## 基本结构

```java
//声明你这个类所处的是哪一个包
package Test;
//文件名必须是 test.java
public class test {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
```

**注意!:main函数必须把参数和返回值这些都写全了,否则编译器无法编译.**

## 基本语法

1. java严格取分字符与字符串,双引号和单引号不能乱用
2. java一个文件只能有一个公有类
3. java公有类的类名必须和文件名一样
4. main方法必须在公有类里面,且必须为static
5. java的方法没有缺省参数

## import

导包必备，java不会写？导就对了，需要啥导啥。面向导包的程序设计——java。

import后面跟上需要导入的包名，之后就可以导入该包里面所有的类。



# javadoc

javadoc是java自带的一套强悍的文档注释,非常好用

```java
/**
* 演示文档注释专用类
* @author 闫辰祥
* @version 1.0
*/
public class test {
  /**
  * 主函数
  * @author 闫辰祥
  * @version 1.0
  * @return 没有返回值
  * @param main函数的参数
  */
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
```

<img src="C:\Users\17966\AppData\Roaming\Typora\typora-user-images\image-20200905192120839.png" alt="image-20200905192120839" style="zoom: 80%;" />

# 基本数据类型

## 值类型

| 关键字  | 大小  | 类型       | 写法举例          |
| ------- | ----- | ---------- | ----------------- |
| byte    | 1字节 | 整型       | byte a = 1;       |
| short   | 2字节 | 整型       | short a = 2;      |
| int     | 4字节 | 整型       | int a = 3;        |
| long    | 8字节 | 整型       | long a = 4L;      |
| float   | 4字节 | 单精度浮点 | float a = 5.0f;   |
| double  | 8字节 | 双精度浮点 | double a = 6.0d;  |
| boolean | 1字节 | 布尔型     | boolean a = true; |
| char    | 2字节 | 字符型     | char a = 'A';     |

## 引用类型

### 强引用

JVM不会回收强引用类型的数据,这个是非常稳的一种数据类型,只有把强引用的引用赋值为null,JVM才会去回收对象.如果内存不足,JVM会抛出OutOfMemoryError异常.

java默认的引用类型就是强引用.

```java
Object obj = new Object(); 
obj = null;
```

### 软引用

在内存足够的时候，软引用对象不会被回收，只有在内存不足时，系统则会回收软引用对象，如果回收了软引用对象之后仍然没有足够的内存，才会抛出内存溢出异常.

### 弱引用

### 虚引用

## 常量

java用final修饰常量

```java
final double PI = 3.1415927;
```

# 数组

## 数组的声明与初始化

### 字面量初始化

```java
int[] chief = {1,1,7};
```

### 构造函数初始化

```java
int[] ning_ning = new int[] {0,7,2,1};
```

### 构造函数分配空间

```java
int[] buf = new int[3];
```

## For-Each循环

和别的语言一样，java也有forEach，可以不使用下标直接访问数组，算是语法糖。

```java
int[] buf = new int[] {1,2,3,4,5,6,7,8,9};
for(int element: buf)
{
	System.out.println(element);
}
```

要注意：element并没有拿到原数组的指针，如果对element修改仅仅影响element的值，而不会影响数组本身。

```java
int[] buf = new int[] {1,2,3,4,5,6,7,8,9};
for(int element: buf)
	element=1;
for(int element: buf)
	System.out.println(element);
//答案是123456789
```



## 多维数组

### 多维数组的定义与初始化

多维数组用多个方括号来表示,初始化方法和上面的一样.

```java
int a[][] = new int[][] {{123},{345}};
int[][] b = {{123},{456}};
```

## 获取行数和列数

数组有length属性，可以直接获取行数，但是列数只能间接获取。

```java
int[][] arr = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
System.out.println(arr.length);
System.out.println(arr[0].length);
```



# 面向对象

面向对象是现代程序设计最重要的思想之一，但是学完之后还是没有对象。

## 类和对象

### 类的结构

java的类里面可以封装**属性，方法，代码块，内部类等**多种结构，下面就是类的一个基本结构

注意:Java中属性会有**默认值**

```java
class Girls{
	//属性
	int age;
	String name;

	//构造方法
	Girls(int age,String name){
		this.age=age;
		this.name=name;
	}
  //普通方法
	void favoriteFood() {
		System.out.print("我喜欢吃蛋黄酱");
	}
	void showInfo() {
		System.out.print("我叫"+name+",今年"+age+"岁");
	}
	
	//代码块  
	{
	   age=13;
	   name="小丛雨";
	}
	
	//内部类
	static class Loli{
		void action() {
			System.out.println("我是萝莉");
		}
	}
}
```

### 构造方法

构造方法是初始化一个对象时，一个自动调用的方法。如果你不写，java也会给你自己造一个空参数的构造方法。java是通过定义和类同名的方法来表示构造方法的。

**注意：java不允许在方法中定义缺省参数！**

```java
public class Girls{
	int age;
	private String name;
	
	Girls(int age,String name)
	{
		this.age=age;
		this.name=name;
	}
}
```

构造方法重载时，如果需要调用其他的构造方法，可以用this()来显式调用。

**不过this()调用的语句，必须放在该构造方法的第一句。**

```java
Girls(int age){
	this.age=age;
}
Girls(int age,String name)
{
	this(age);
	this.name=name;
}
```

### 代码块

代码块就是用一个大括号封装起来的代码，java不允许在构造函数里面写缺省参数，但是如果没有这个功能实在是非常非常不方便。这时候我们就可以利用代码块来进行属性的初始化。

```java
class Girls{
	int age;
	String name
	//代码块可以用来初始化属性
	{
	    age=13;
	    name="小丛雨";
	}
}

```

代码块分为两种，一种是我们上面提到的普通代码块，这种代码块**随着对象创建而执行**，也就是说，对象创建之后，就会来执行代码块里面的内容，一般用于初始化对象的属性。

另一种是static修饰的静态代码块，这种代码块**随着类的创建而执行**，也就是说在类创建之后，就会来执行，这个很明显就是来初始化类的静态属性的。

### 内部类

内部类里面也可以写属性，方法，代码块和内部类。我们这里不讲他作为类的特点，我们主要来谈谈，他作为一个内部类的特点。其实我在这个文档里面写的代码基本上都是内部类，，，因为开很多文件很麻烦的说。

在实例化内部类的时候，最好用外部类点内部类来访问，但是main和内部类在对于同一个类中时，不需要点也可以。

实例化内部类有两种办法，一种是声明为静态，这样main方法就可以直接访问静态内部类了。

```java
public class Girls{
	//静态内部类
	static class Loli{
		void action() {
			System.out.println("我是萝莉");
		}
	}
	public static void main(String[] str) {
		Girls.Loli loli = new Girls.Loli();
		loli.action();
	}
}
```

**new内部类的时候，需要先new外部类再new内部类**

**格式为：new 外部类().new 内部类();**

先创建匿名外部类，之后在用外部类间接创建内部类。

```java
public class Girls{
	//普通内部类
	 class Loli{
		void action() {
			System.out.println("我是萝莉");
		}
	}
	public static void main(String[] str) {
    //用两个new来实例化内部类
		Girls.Loli loli = new Girls().new Loli();
		loli.action();
	}
}
```



### this

### 类的静态属性和方法

如果一个类中某个属性或方法是需要所有对象都能共享的，那么就可以声明为静态属性或方法。比如说，人类这个类里面有一个星球的属性，而人类这个类所有实例化的对象中，星球都是地球，这样就没必要为每一个对象都分配一个这个属性了。直接把星球属性设置为静态，这样全人类都可以共享这个属性。**声明静态用static关键字。**

**要想使用静态变量，必须把当前类也声明为静态类**。

```java
public static class Human {
	static String Planet = "地球";
}
//不管是谁，打印的结果都是地球，因为这个是人类共有的属性
public static void main(String[] args) {
  Human me = new Human();
  Human you = new Human();
  System.out.println(me.Planet);
  System.out.println(you.Planet);
}
```

静态属性/方法有以下的特性：

- 静态属性/方法是跟随类一起创建的，比对象创建的早。在没有对象的时候也能使用静态属性和方法。
- 因为类只会加载一份，所以类的静态属性/方法只有一份。
- 因为这个静态变量属于类，所以可以用类直接调用，而且建议这样做。
- 因为静态属性是类所有的，所以静态方法只能调用静态方法和属性。



### JavaBean

JavaBean是一种特殊的java类，需要满足如下三点：

1. 类的访问权限为public
2. 有一个无参公共的构造函数
3. 有属性和对应的set，get方法。

## 封装与隐藏

### 访问控制权限

封装和隐藏是面向对象里面基本思想之一。建议把数据都封装在类的内部，把类都封装在包里面，把所有包都封装在一个工程里面。这样可以提高程序的内聚，降低耦合。

java的访问控制的关键字有这么四个:public，private，protected，缺省。

缺省就是啥都不写。

| 修饰符 | 类内访问 | 同一个包访问 | 不同包的子类访问 | 同一个工程访问 |
| ------ | -------- | ------------ | ---------------- | -------------- |
| private | √ |              |                  |                |
| default | √ | √ |                  |                |
| protected | √ | √ | √ |   |
| public | √ | √ | √ | √ |

首先说一下这几个名词的意思

- 类内访问：

  就是指可以在类内部调用，比如方法调用某个属性。

- 同一个包访问：

  java写代码都是写在包里面的，首先建一个包，然后里面写class。只要可以在同一个包内访问，那你这个包底下的class就可以互相调用数据。

- 不同包的子类访问：

  在不同包里面，虽然private和缺省不能访问，但是子类可以使用其他包protected级别的数据。

- 同一个工程访问

  在一个工程内，就算在不同的包，也可以调用对方类的数据。





### 属性的get和set方法

为了避免public权限的属性被直接赋值或者调用，我们一般都把属性设置为private。但是问题又来了，这个东西我本来是想让你调用的，但是我又不想让你直接调用，那该怎么办呢？

这时候我们就可以给private类型的属性设置set方法和get方法，只给外界暴露接口，而不是直接暴露数据。

```java
private String name;

public String getName() {
	return name;
}

public void setName(String name) {
	this.name = name;
}
```

### 包装类

#### 基本数据类型转化为包装类

首先是基本数据类型转化为包装类，

## 继承

java继承和别的语言差不多，会继承父类的非private的方法和属性，包括protected和public。

Object类是java中所有类的父类，是老祖宗。

### 基本结构

java不支持多继承，但是支持单继承。也就是说一个儿子一个爹，但是一个爹可以有很多儿子。

虽然子类会继承父类的所有属性和方法，但是不能去访问父类的private的方法。

```java
class 父类 {
}
 
class 子类 extends 父类 {
}
```

### 构造函数的继承

在继承构造函数的时候继承父类的构造函数，通过super关键字，java编译器会自动找到参数匹配的父类构造函数.

```java
class Loli{
  public int age;
  Loli(int age){
    this.age = age;
  }
}
class YouNv extends Loli{
  YouNv(int age) {
    super(age);
  }
}
```

super就相当于父类的this，如果想显示调用父类的方法，可以用`super.favoriteFood(food);`

### 接口(interface)

java不允许多继承，这虽然让继承变得很简单。但是也大大限制了java类的功能。比如说助教类，到底是继承学生类呢，还是继承老师类呢？是不是都不合适，这时候就应该两个都继承才好。为了弥补这种缺陷，java提供了接口，以便实现多继承的功能。

在java里面接口和类的地位是一样的，所以怎么样使用类就可以怎么样使用接口。但是java毕竟不允许多继承，所以**接口代表的是功能，而不是某种类**。比如说把教学和上学这两种功能封装起来，拥有这两种功能特点的类就是助教了。但是类仅仅是指某一类事物，比如说老师和学生，他们是具体的某样东西，而不是抽象的功能。

不过接口和类还是有诸多区别的，首先看看基本结构。

```java
//教学接口
interface Teach{
	public static final int tea_id = 0;
	public static void earMoney() {
		System.out.println("赚钱");
	}
}
//学习接口
interface Study{
	public static final int stu_id = 0;
	public abstract void readBooks();
}
//助教类，实现了上面两个接口
public class TeachStudents implements Teach,Study {
	public static void earMoney() {
		System.out.println("赚钱");
	}
	
	public void readBooks(){
		System.out.println("读书");
	}
	
	public static void main(String[] args) {
		TeachStudents zhangSan = new TeachStudents();
		TeachStudents.earMoney();
		zhangSan.readBooks();
	}
}
```

接下来详细讲讲里面的具体内容：

- 接口不能拥有构造方法！所以接口不可以拥有实例对象，这个很好理解，老师类是某一类人，是一个名词，他的实例化对象就是某一个人。但是教学是一个动词，动词不可能再划分了吧。吃饭接口的实例化是什么？某一个吃饭？？？可爱的这个形容词接口的实例化是什么？某一个可爱的？？是不是都不合适，所以说动词和形容词一般都是用于接口的，而这种接口从语法语义上来讲都不应该有实例对象。（实际上很多英文教材都用的是 IS A这种思想，不过这里我就不多讲了）
- 接口所有方法都是隐式抽象的，也就是说如果不加abstract，编译器也会自动给所有方法前面加上abstract修饰符。
- 接口中只允许public权限
- 接口也可以多继承接口

说了这么多实际上接口用起来语法非常简单，**接口只允许常量属性，抽象方法和静态方法存在**。也就是说所有变量前面都要加一大堆修饰符。所以为了简化起见，我们可以省略这些关键字，就如我刚才说的，编译器会自动加上这些修饰符。

```java
interface Study{
	public static final int stu_id = 0;
	public abstract void readBooks();
}
//等价于
interface Study{
	int stu_id = 0;
	void readBooks();
}
```

但是静态方法不能简写，还得老老实实把方法体写上。

最后说一下，继承可以和实现同时使用，顺序是先继承后实现

```java
public class TeachStudents extends Object implements Teach{
	public static void earMoney() {
		System.out.println("赚钱");
	}
}
```



### final关键字

final关键字有三个作用。

1. 修饰类时，代表该类不能被继承

java有一个老祖宗Object，所有类都是由它继承而来。java也设计了一个辈分最低的类，也就是没有任何子类的类，我们用final关键字来修饰这个类，代表这个类不能拥有子类。

```java
final class Girls{}
//下面的代码会报错：The type lolis cannot subclass the final class Girls
//因为不能继承final类
public class lolis extends Girls{}
```

2. 修饰方法时，代表该方法不能被重写

```java
public class Girls{
	public final void showInfo() {
		System.out.print("我是父类");
	}
}
//编译器会报错：Cannot override the final method from Girls
public class lolis extends Girls{
	public void showInfo() {
		System.out.print("我是子类");
	}
}
```

3. 修饰属性时，代表属性为常量。java没有const很不习惯，说起来JavaScript也没有，，，还是c#好用。

```java
final double PI = 3.1415927;
```



## 多态

java的多态确实是很丰富多彩，<del>而且比C++简单多了</del>.多态分为静态多态和动态多态。

在编译期间由编译器自己判断所调用的方法，这种就是静态多态，靠方法重载实现。

第二种就是通过动态绑定实现的动态多态，下面会详细讲解。

### 方法重载

方法和函数都能重载**如果定义的新方法和别的方法名一样,但是参数类型或者数目不一样,那么这个新方法就是重载方法.**

```java
void favoriteFood() {
		System.out.print("我喜欢吃蛋黄酱");
}
void favoriteFood(String food) {
		System.out.print("我喜欢吃"+food);
}
```

### 可变长形参的重载

有的时候，输入的变量数量可能不erq确定，假如有可能为3个,也有可能到100个,为了避免写太多重载,java提供了一个可变数量的形参.可以匹配多个参数,而且只能放到末尾.(很好理解吧,可变形参放前面,后面放一个普通参数,那编译器就不知道到底是把所有实参都给前面,还是说给最后面留一个,会造成歧义)

这个可变长形参的用法和数组一样,用for来遍历.

```java
void favoriteFood() {
	System.out.print("我喜欢吃蛋黄酱");
}
void favoriteFood(String food) {
	System.out.print("我喜欢吃"+food);
}
static void favoriteFood(String... food) {
	for(int i=0;i<food.length;i++)
		System.out.print("我喜欢吃"+food[i]);
}
```

其实在以前没有这种特性的时候,程序员们都是用数组来间接实现可变长参数的.

```java
void favoriteFood(String[] food) {
	for(int i=0;i<food.length;i++)
		System.out.print("我喜欢吃"+food[i]);
}
```

就这样.

但是要注意,现在java编译器不允许你即用数组,又用可变长参数.这两种方法只能用一种.

### 方法重写

如果刚才重载的时候，把方法名和形参列表都写的一样，那么就会发生方法的重写。但是一个类里面不能写两个完全一样的方法，所以方法重写只能由子类重写父类来实现。

方法重写有以下的要求：

- 重写方法只能由子类重写父类方法实现
- 重写的方法，必须与原方法名字和形参列表一样。
- 子类重写时，权限修饰符的范围必须一样或者更大。
- 子类不能重写父类中private的方法。
- 重写方法的返回值必须是父类返回值的子类，或者一样。
- 子类重写方法所抛出的异常，小于等于父类的异常类型。

要注意，属性不能被重写，父类有一个name属性，子类也有一个name属性，那么两者不会冲突，各用各的，可以用this和super区分。

### 重写方法的动态绑定

如果子类重写了父类的方法，之后用父类去引用子类的对象。那么在调用这个方法的时候，到底是执行父类的呢，还是子类的呢？

```java
//父类
public class Girls {
	public void showInfo() {
		System.out.print("我是父类");
	}
}
//子类
public class lolis extends Girls{
  public void showInfo2() {
		System.out.print("我也是子类");
	}
	public void showInfo() {
		System.out.print("我是子类");
	}
}
//main方法
public static void main(String[] args) {
  Girls congYu = new lolis();
  congYu.showInfo();
}
```

如上所述，虽然声明的类型是Girls，但是实际上congYu所调用的方法却是lolis的。

但是如果你有调用上面那个showInfo2()，你就会发现编译器居然会报错，说是没有定义？明明说好了运行时会采用lolis的行为啊？为什么现在又不让用了？

![image-20200920234131432](img/image-20200920234131432.png)

其实这个就是动态绑定的特点。你在编译的时候声明的类型为Girls，那么编译器就认为你这个对象就是Girls类型的，Girls类型当然没有这个showInfo2()方法喽，所以会报错。也就是说**编译看左边类型，运行看右边类型**。所以说把这种动态绑定对象类型的技术就叫做动态绑定。

ps： **父类中被重写的方法叫做虚方法**，但是感觉C++这边用的比较多，java里面不是很强调这个词。

### 向下转型

刚才我们说过，动态绑定的时候，得用父类的类型来接受子类的对象，这就导致了一个严重的问题，这个对象被编译器认为是父类类型，所以只允许调用父类的方法，其实内存里面是有子类的方法的，但是现在这么一整，等于把子类直接阉割掉了。那这种动态绑定不要也罢(????龙王既视感???)。

为了让动态绑定不这么鸡肋，我们可以使用向下转型的技术。其实就是使用**强制类型转换**。

把范围小的赋值给大的，可以自动转型，比如说把子类赋值给父类。而把父类缩小为子类，则需要强制类型转换。

```java
public static void main(String[] args) {
	Girls congYu = new lolis();
	lolis congYu2 = (lolis)congYu;
	congYu2.showInfo2();
}
```

就像这种，在使用时强行转化为子类，就可以调用子类的方法了。但是别瞎转，你明明是lolis子类，如果非要转化成御姐类，那运行时会直接抛出异常。

### instanceof关键字

就如我刚刚说的，congYu是一个lolis类型的对象，所以强行转换为lolis是没有问题的。但是如果强行转化为其他类呢？编译时当然不会报错了，因为这个操作是符合语法的。但是运行时会报错，抛出ClassCastException异常。就是因为你这个类型不匹配。

为了更加安全的向下转型，我们可以利用instanceof运算符来判断。

instanceof是一个二元运算符，`A instanceof  B`，就代表A是B的子类。如果是返回true，否则false。

```java
public static void main(String[] args) {
	Girls congYu = new lolis();
	if (congYu instanceof lolis) {
		lolis congYu2 = (lolis)congYu;
		congYu2.showInfo2();
	}
}
```

## 抽象

在实际开发中，父类都是会一层层封装继承下去的，这就导致父类越来越抽象，子类越来越具体。这时候就会出现一个现象，那就是父类的方法不再具有任何实际的意义，比如说生物类，生物类可以有一个行为的方法，但是不同类继承之后对这个方法的重写千差万别，不论父类写什么都不合适，还不如不写，干脆让子类自己继承呢。

```java
class Organism{
	void action() {
		//这里应该填什么才合适呢？
	}
}
class Human extends Organism{
	void action() {
		System.out.println("我会写代码");
	}
}
class Cat extends Organism{
	void action() {
		System.out.println("我会喵喵喵");
	}
}
```

### 抽象方法和抽象类

为了解决这个问题，我们可以用abstract关键字修饰父类的action方法，并且去掉大括号，让它成为抽象方法，强制要求子类重写父类的方法。

```java
abstract class Organism{
	abstract void action();
}
```

**如果这个类中有抽象方法，那么这个类就是抽象类**。抽象类有下面几个特点：

- 没有实例对象：

  很好理解，因为抽象方法就没有函数体，无法实例这个方法，所以也无法实例对象。

- 可以没有抽象方法：

  有抽象方法必然是抽象类，但是没有抽象方法也可以用abstract来修饰类。

  ```java
  //没有抽象方法也可以成为抽象类
  abstract class Organism{
   void action();
  }
  ```

- 子类会继承父类的抽象方法：

  也就是说如果子类没有重写父类的抽象方法，那么子类也是抽象类，直到某一个子类把所有抽象方法都重写之后，才能有对象。

### 匿名内部类和匿名对象

首先看看匿名对象吧，这个我们之前其实已经用了很多了。

```java
Girls[] manyGirls = {new Girls(),new Girls()};
```

直接new出来的对象就是一个匿名对象，因为这个对象没有名字，直接使用的。像这种需要大量临时对象的时候，就需要使用匿名对象，要不然一个一个声明实在太麻烦了。

之后就是匿名内部类了，匿名内部类是通过重写抽象父类实现的。下面看代码。

```java
abstract static class Organism{
  abstract void action();
}
	
public static void main(String[] str) {
  new Organism() {
    void action() { System.out.println("我是人类"); }
  }.action();
}
```

抽象类是不能有实例对象的，这个new其实也并不是new抽象类的对象，而是先去构造一个匿名子类，最后new这个匿名子类。

这种匿名内部类也可以被继承，或者作为实际参数传递。用法非常灵活。但是有以下限制：

- 匿名子类必须重写父类所有抽象方法
- 匿名子类不能拥有构造函数，毕竟是一次性的，，
- 匿名子类不能拥有静态属性或方法。

# 异常

## 分类

Java程序在执行过程中所发生的异常事件可分为两类:

- Error：Java虚拟机无法解决的严重问题。如:JVM系统内部错误、资源
  耗尽等严重情况。比如:StackOverflowError和OOM。一般不编写针对性
  的代码进行处理。
- Exception：其它因编程错误或偶然的外在因素导致的一般性问题，可以使
  用针对性的代码进行处理。例如:
  - 空指针访问
  - 试图读取不存在的文件
  - 网络连接中断
  - 数组角标越界

ERROR的错误我们不用去管，我们只用去处理Exception就行了。

java的Exception也分为两类：

- checked异常：也叫做受检异常，指的是java虚拟机把源代码编译成字节码时出现的异常。也就是编译异常。
- RuntimeException异常：指的是运行代码时出现的异常。



## 异常处理

异常处理有两种方法，一种是通过`try catch`语句捕获并处理，另一种是通过`throw`直接抛出。

### try catch

首先说说`try catch`吧，一般当错误比较少，自己可以解决的时候，就可以catch异常，自己写处理语句。

```java
try {
  int a=1;
  int b=0;
  int c=a/b;
  System.out.println(c);
} catch (Exception e) {
  System.out.println("出现异常！");
}
```

如果异常可能有很多种，不能确定到底是哪个错了。或者想明确指出异常种类时，可以写多条catch，跟if-else有点像。

```java
try {
  int[] a = {1,0};
  int c=a[0]/a[2];
  System.out.println(c);
} catch (ArithmeticException a) {
  System.out.println("出现除0异常！");
} catch (ArrayIndexOutOfBoundsException a) {
  System.out.println("出现数组越界异常！");
}
```

在catch语句之后还可以声明一个finally语句，用于收尾清理的工作。注意：**无论是否发生异常，finally 代码块中的代码总会被执行。**因为无论你有没有异常，像一些释放指针，释放资源的工作还是必须做的。比如关闭文件，关闭I/O流等工作。在C++中尤其明显，java里面因为没有显式指针，所以老是忘记释放资源。。。

```java
String string = new String("hello world");
try {
	char c=string.charAt(string.length());
	System.out.println(c);
} catch (StringIndexOutOfBoundsException s) {
	System.out.println("出现字符串越界异常！");
} finally {
	//回收字符串指针。
	string = null;
}
```

### throw

如果这个类异常很多，或者很难处理，或者你不想处理，就可以用throw抛出，但是并不做处理。这个异常会转交给上一级，上一级可以用try catch来接收这个异常。

我用JDBC的一个例子举例吧，这个是实际开发中用到的，比较有代表性。

```java
	public static void main(String[] args) throws Exception {
			Class.forName("com.mysql.cj.jdbc.Driver");
			Connection connect = DriverManager
					.getConnection("jdbc:mysql://localhost:3306/TwoDimensions?serverTimezone = GMT", "root", "4399");
			Statement stmt = connect.createStatement();
			String sql= "select * from girls";
			ResultSet rs = stmt.executeQuery(sql); 
			while (rs.next()) {
				System.out.println(rs.getString("loli_name"));
			}
			rs.close();
			connect.close();
			stmt.close();
	}
```

如果不用throw，就得对每一条语句都做一个try catch，写到爆炸，而且这个异常不处理也可以，所以就throw了，不用管。

**在继承的时候，子类的异常范围必须比父类要小**。

## 手动抛出异常

设想这样一个情况，我需要输入妹子的年龄，但是我手滑输入了-14岁，这在编译和运行阶段都不会报错，但是确确实实不符合我的设想，我就可以手动抛出一个异常，以提示错误信息。

这个异常是需要手动接收的。

```java
//构造方法
Girls(int age,String name) throws Exception{
	if(age>16)
	{
		throw new Exception("太老了！！！绝对不允许！！");
	}
	this.age=age;
	this.name=name;
}
//main函数
public static void main(String[] str) {
		try {
			new Girls(18,"123");
		} catch (Exception e) {
			e.printStackTrace();
		}
}
```

## 自定义异常类

正因为我们有上面手动抛出异常的需求，所以我们抛出异常一直用Exception类就显得非常违和，比如说这个是年龄的异常，我们就希望有一个年龄的异常，这样子就更加直观了。但是java自己肯定没有这个异常类，所以我们就需要自己定义。

```java
//自定义的年龄异常
class OldException extends Exception{
	OldException(){
		super("太老了！！！绝对不允许！！");
	}
}

// 构造方法
Girls(int age, String name) throws OldException {
  if (age > 16) {
    throw new OldException();
  }
  this.age = age;
  this.name = name;
}

//main方法
try {
	new Girls(18, "123");
} catch (Exception e) {
	e.printStackTrace();
}
```

一般来说，我们的异常类只需要把父类继承过来就可以了。构造方法也直接调用父类的就可以了。我们写这个自定义异常类目的仅仅是修改这个类名，这样在抛出的时候就更加有可读性，并不是真的自己写一个异常类。

# 多线程

## 基本概念

- 程序：

  就是你写的代码。

- 进程：

  就是运行起来的代码。

- 线程：

  一个进程可以开创多个线程，一个线程就是程序运行是最小单位，比如说一个游戏进程里面可能有一个线程负责计算渲染，一个负责计算碰撞，一个负责网络通信。总而言之，就是让不同的代码分别干不同的事情。

- 并行：

  多个CPU同时处理多个任务。

- 并发：

  指一个CPU同时执行很多很多任务，但是CPU执行速度太快了，所以几乎就是同时进行。

## java多线程的创建

### 继承Thread类

1. 继承Thread类，创建子类
2. 重写Thread类的run()
3. 创建Thread类的子类的对象
4. 通过此对象调用start()

```java
//1.继承Thread类
public class ThreadTest extends Thread{
	//2.重写run方法
	public void run() {
		System.out.println("hello Thread!");
	}
  
	public static void main(String[] args) {
		//3.实例化子类并调用start方法。
		new ThreadTest().start();
    //或者可以写全
    //ThreadTest thread = new ThreadTest();
    //thread.start();
	}
}
```

我们规定启动线程需要使用start方法，那调用run方法会怎么样呢？其实也不会报错，但是run方法就不会创建新的线程了，直接在主线程执行了。

### 实现Runnable接口

1. 实现Runnable接口
2. 重写run()方法
3. 创建实现类的对象
4. 用这个对象作为形参，构造一个Thread对象
5. 调用Thread对象的start方法。

```java
//1.实现Runnable接口
public class ThreadTest2 implements Runnable{
  //2.重写run()方法
	public void run() {
		System.out.println("hello Thread!");
	}

	public static void main(String[] args) {
    //3.创建实现类的对象
		ThreadTest2 threadTest2 = new ThreadTest2();
    //4.用这个对象作为形参，构造一个Thread对象
		Thread thread = new Thread(threadTest2);
    //5.调用Thread对象的start方法。
		thread.start();
	}
}
```

### 实现Callable接口

Callable接口比Runnable接口更为强大。

- 相比run()方法，可以有返回值
- 方法可以抛出异常
- 支持泛型的返回值
- 需要借助FutureTask类，比如获取返回结果

这个实现方法比较复杂，请仔细阅读步骤：

1. 实现Callable接口
2. 重写call()方法
3. 创建实现类的对象
4. 用实现类的对象构造FutureTask类的对象
5. 用FutureTask的对象创建Thread的对象。
6. 调用start方法。

```java
//1.实现Callable接口
public class ThreadTest3 implements Callable{
	//2.重写call()方法
	public Object call() throws Exception {
		System.out.println("Callable接口创建线程。");
		return null;
	}

	public static void main(String[] args) {
		//3.创建实现类的对象
		ThreadTest3 threadTest3 = new ThreadTest3();
		//4.用实现类的对象构造FutureTask类的对象
		FutureTask futureTask = new FutureTask(threadTest3);
		//5.用FutureTask的对象创建Thread的对象。
		Thread thread = new Thread(futureTask);
    //6.调用start方法。
		thread.start();
	}
}
```

call方法允许有返回值，如果需要可以通过futureTask对象的get方法来获取

```java
futureTask.get();
```

### 使用线程池创建

经常创建和销毁、使用量特别大的资源，比如并发情况下的线程，对性能影响很大。如果提前创建好多个线程，放入线程池中，使用时直接获取，使用完放回池中。可以避免频繁创建销毁、实现重复利用。类似共享单车，你要用车，你就用，用完再给别人，而不是你用完自己拿回家去了，那别人咋办？强烈反对这种没素质的行为，良好的社区环境需要大家共同维护。

1. 建造线程池
2. 用Runnable或者Callable的实现类对象创建线程
3. 关闭线程池

```java
public class ThreadTest4 implements Runnable {

	public void run() {
		System.out.println("使用线程池创建线程。");
		
	}

	public static void main(String[] args) {
		//1.建造指定数量的线程池
		ExecutorService service =Executors.newFixedThreadPool(10);
		//2.建造线程
		service.execute(new ThreadTest4());//传递Runnable对象
		//service.submit();//传递Callable对象
		//3.关闭线程池
		service.shutdown();
	}
}

```



## 线程常用方法

| 方法              | 说明                                            |
| ----------------- | ----------------------------------------------- |
| start()           | 启动线程                                        |
| run()             | 线程具体所作的操作                              |
| currentThread()   | 返回当前运行的线程                              |
| getName()         | 获取当前线程名                                  |
| setName("string") | 设置线程名                                      |
| join()            | a线程中调用b.join()，就会阻塞a线程，直到b运行完 |
| sleep(long time)  | 让调用的线程进入阻塞态                          |

## 线程优先级

java线程优先级一共有10档，其中默认五档，最高10，最低1。java定义了3个默认的宏来表示一些代表性的优先级。

- MAX_PRIORITY: 10
- MIN_PRIORITY: 1
- NORM_PRIORITY: 5   默认优先级

```java
ThreadTest test = new ThreadTest();
//用java的宏定义
test.setPriority(MAX_PRIORITY);
//自己自定义
test.setPriority(5);
```

## 线程的生命周期

java用一个枚举类State来列举五种状态。具体请看操作系统原理。

```java
public enum State {
        /**
         * 创建态：当新的Thread对象创建时
         */
        NEW,

        /**
         * 运行态：执行该方法时
         */
        RUNNABLE,

        /**
         * 阻塞态：线程被挂起，临时中断运行态时
         */
        BLOCKED,
  
  
        /**
         * 就绪态：调用start方法后，在线程队列等待时间片分配的时候
         */
        WAITING,

        /**
         * Thread state for a waiting thread with a specified waiting time.
         * A thread is in the timed waiting state due to calling one of
         * the following methods with a specified positive waiting time:
         * <ul>
         *   <li>{@link #sleep Thread.sleep}</li>
         *   <li>{@link Object#wait(long) Object.wait} with timeout</li>
         *   <li>{@link #join(long) Thread.join} with timeout</li>
         *   <li>{@link LockSupport#parkNanos LockSupport.parkNanos}</li>
         *   <li>{@link LockSupport#parkUntil LockSupport.parkUntil}</li>
         * </ul>
         */
        TIMED_WAITING,

        /**
         * Thread state for a terminated thread.
         * The thread has completed execution.
         */
        TERMINATED;
}
```

## 线程安全

### 问题提出

我们以一个实例来引出线程安全的问题。

假设现在有20张票，然后后台有两个抢票线程在抢票。这时就可能导致线程安全问题了。我第一个线程刚刚抢到一个num，然后还没来得及调用num--的时候，你第二个线程就也来抢这个了。这就导致两个线程可能会拿到一样的票。

```java
public class ThreadSecure implements Runnable{
	public static int num = 20;
	public void run() {
		while(num>0) {
			System.out.println(Thread.currentThread().getName()+"：得到了第"+num+"号票");
			num--;
		}
	
	}

	public static void main(String[] args) {
		ThreadSecure thrSecure = new ThreadSecure();
		Thread thread = new Thread(thrSecure);
		Thread thread2 = new Thread(thrSecure);
		thread.setName("1号线程");
		thread.start();
		thread2.setName("2号线程");
		thread2.start();
	}
}
```



<img src="img/image-20200924204416401.png" alt="image-20200924204416401" style="zoom:67%;" />

同样的，即使你把num--提到前面问题也不会解决。因为这样子就不是从20开始抢票了，而是直接先减之后再打印信息，也就是从19开始了。

```java
while(num>0) {
			num--;
			System.out.println(Thread.currentThread().getName()+"：得到了第"+num+"号票");
}
```

<img src="img/image-20200924204451895.png" alt="image-20200924204451895" style="zoom:67%;" />

而且这时候反而会出现编号越界。

### 同步代码块

之所以出现这种线程安全问题，就是因为在同一时间，数据被多次访问了。其实也很好解决，当一个线程访问某些代码块的时候，把这个代码块锁死就可以了。这就好比去上厕所，一旦有人进去，厕所那个门前面就会变红。这就代表里面有人了，你其他人先别着急进去，这就叫那个锁就是**同步代码块**，而开锁的钥匙就是**同步监视器**。而那个如果厕所没有这个锁，我刚进去准备处理数据，你也进来了，咱俩大眼瞪小眼，这就叫线程安全问题。（说起来莫名想到精子和卵子，虽然同一时刻有很多精子访问卵子，但是最终只能有一个精子访问到，不能被多次访问）

那我们来康康具体怎么解决。

```java
//同步监视器就是key
public static Object key = new Object();
public void run() {
	while (true) {
    //同步代码块就是锁
		synchronized (key) {
			if (num>0) {
				System.out.println(Thread.currentThread().getName() + "：得到了第" + num + "号票");
				num--;
			}else {
				break;
			}
		}
	}
}
```

其实很简单，我们有线程安全是因为访问了共享数据，所以只需要给有共享数据的代码块加上一个同步锁synchronized就可以了。原理就是进入代码块的线程会用同步监视器锁死这个代码块，别人都进不来，直到这个线程运行完释放同步监视器，其他线程才能去抢钥匙。这个同步锁需要传一个参数，这个参数就是同步监视器，也就是钥匙。这个参数是随便一个共享对象就可以。很好理解，大家合用一把锁，也只能有一个公有的钥匙，谁进厕所谁把钥匙拿着，这样别人就进不去了。如果你这个对象不是公有的，大家都有钥匙，那你这个锁就形同虚设了。

另外大家其实已经发现我把代码里面的`while(num>0)`改成了`while (true) `和`if-else`的结构。因为如果用`while(num>0)`，那么一旦线程进去把锁一加，直接就一口气while完了，根本轮不到别的线程进去。所以不要给while加同步锁。

![image-20200924203726656](img/image-20200924203726656.png)

另外说一下，多线程的结果每次执行都不一样，如果你遇到只有1号线程或者2号线程执行其实很正常，多刷几次就有了。

最后再说一下，synchronized要传递一个公有对象，自己建一个Object的对象诚然是可以的，但是有一点点麻烦。还记得实现Runnable接口的特点吗？首先创建一个公有的实现类的对象，之后再构建Thread对象。这时候就已经有一个公有的实现类对象了，所以对于用实现Runnable接口方式构建的对象，可以直接传递this指针。也就是将公有的实现类对象作为key来管理同步锁。

```java
public void run() {
	while (true) {
		synchronized (this) {
			if (num>0) {
				System.out.println(Thread.currentThread().getName() + "：得到了第" + num + "号票");
				num--;
			}else {
				break;
			}
		}
	}
}
```

这个方法仅限于实现Runnable接口，对于继承Thread的对象来说，我们就不能用这个了。因为Thread类的每个对象都用的是自己的run()方法，你this传进去，大家的key还是各自的对象。所以这就起不到一个锁一个钥匙的效果。对于这种情况，我们可以用类对象作为参数。因为一个类只有一个类对象，所以可以作为key。

```java
public class ThreadTest extends Thread {
	public static int num = 20;

	public void run() {
		while (true) {
			synchronized (ThreadTest.class) {
				if (num > 0) {
					System.out.println(Thread.currentThread().getName() + "：得到了第" + num + "号票");
					num--;
				} else {
					break;
				}
			}
		}
	}

	public static void main(String[] args) {
		ThreadTest thread = new ThreadTest();
		ThreadTest thread2 = new ThreadTest();
		thread.setName("1号线程");
		thread.start();
		thread2.setName("2号线程");
		thread2.start();
	}
}
```

### 同步方法

这个其实就是对同步代码块的封装。如果一个同步代码块的内容可以抽出来封装成一个方法的话，那就变成了同步方法。

同样的，同步方法用synchronized关键字来修饰，此时就不需要传递公有对象了。因为编译器会自己传递默认参数，根据你对方法的不同定义，编译器会传递不同的默认参数。

首先看看继承Thread类时同步方法的使用说明。

```java
public class ThreadTest extends Thread {
	public static int num = 20;
	
	//静态方法默认传递 类.class作为同步监视器。
	synchronized static void buy() {
		if (num > 0) {
			System.out.println(Thread.currentThread().getName() + "：得到了第" + num + "号票");
			num--;
		}
	}

	public void run() {
		while (num>0) {
			buy();
		}
	}

	public static void main(String[] args) {
		ThreadTest thread = new ThreadTest();
		ThreadTest thread2 = new ThreadTest();
		thread.setName("1号线程");
		thread.start();
		thread2.setName("2号线程");
		thread2.start();
	}
}
```

首先一定要声明静态方法，因为不这样的话每个Thread的对象都有有一个自己的buy()方法，起不到一把锁一个钥匙的作用。只有静态方法才能保证所有对象公用一个钥匙。静态方法编译器默认采用类.class作为同步监视器（钥匙）。

另一种我想大家已经猜到了吧。就是直接给方法加上synchronized修饰符就行了，因为实现类的对象是公有的，所以buy()方法也是公有的，此时默认用this作为同步监视器。

```java
public class ThreadTest implements Runnable{
	public static int num = 20;
  //非静态方法默认传递 this作为同步监视器
	public synchronized void buy() {
		if (num>0) {
			System.out.println(Thread.currentThread().getName() + "：得到了第" + num + "号票");
			num--;
		}
	}
	public void run() {
		while (num>0) {
			buy();
		}
	}

	public static void main(String[] args) {
		ThreadTest thrSecure = new ThreadTest();
		Thread thread = new Thread(thrSecure);
		Thread thread2 = new Thread(thrSecure);
		thread.setName("1号线程");
		thread.start();
		thread2.setName("2号线程");
		thread2.start();
	}
}
```

### Lock

除了刚才那些自动加锁的方法，我们也能手动加锁。首先new一个ReentrantLock的对象，之后调用这个对象的lock方法开启锁，用unlock手动关闭。

```java
ReentrantLock lock = new ReentrantLock();
public void run() {
	while (num>0) {
		try {
			lock.lock();
			if (num>0) {
				System.out.println(Thread.currentThread().getName() + "：得到了第" + num + "号票");
				num--;
			}
		} finally {
			lock.unlock();
		}
	}
}
```



## 线程死锁

- 不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁
- 出现死锁后，不会出现异常，不会出现提示，只是所有的线程都处于阻塞状态，无法继续

还是用代码来说吧。有一说一我觉得我这个例子相当完美，请允许我小小地骄傲一下。(✿◡‿◡) ，o(*￣▽￣*)ブ。

话说很久很久以前，在大唐西市有一家卖黄桥烧饼的，物美价廉，大家是络绎不绝，但是店主有一个规矩，先交钱后拿货。而这天有一个年轻的少侠也云游到了这里，这少侠平时为人豪爽行侠仗义，但是也有一个规矩：先拿货后交钱。这下可谓是无巧不成书啊。这小伙子正巧想吃黄桥烧饼，一到摊子前面，这不就准备买饼了嘛。他首先调用start方法，然后执行Customer的run方法，这时候他就拿到了moneykey的同步监视器，接着告诉摊主：“先交货”，因为这时候goodkey不在他手里，所以线程阻塞。

话说另一半摊主也在同步的工作，因为是并行运算嘛，大家各干各的。摊主与此同时也拿到了goodkey的同步监视器，然后发现自己没有拿到moneykey，也就是没拿到钱，然后也阻塞了。

这时候问题就来了，货物goodkey在摊主手里，而钱moneykey在买家手里。但是摊主说，你先把moneykey给我我才能把goodkey给你，而少侠说那你得先把goodkey给我我才能把moneykey给你。这样一来两个线程就都阻塞了。谁都不能运行了。

```java
class Customer extends Thread {
	public void run() {
		DeadLock deadLock = new DeadLock();
		deadLock.good();

	}
}

class Businessman extends Thread {
	public void run() {
		DeadLock deadLock = new DeadLock();
		deadLock.money();

	}
}

public class DeadLock {

	static Object moneykey = new Object();
	static Object goodkey = new Object();

	void money() {
		synchronized (goodkey) {
			System.out.println("先交钱");
			synchronized (moneykey) {
				System.out.println("拿到钱了，给你货");
			}
		}
	}

	void good() {
		synchronized (moneykey) {
			System.out.println("先交货");
			synchronized (goodkey) {
				System.out.println("拿到货了，给你钱");
			}
		}
	}

	public static void main(String[] args) {
		Customer customer = new Customer();
		Businessman businessman = new Businessman();
		customer.start();
		businessman.start();

	}
}
```



![image-20200925135607904](img/image-20200925135607904.png)

可以看到程序卡在了这里，直接死循环。接下来的生意也没法做了。

要问怎么办？切记不要用嵌套的同步代码块，不然很可能线程死锁。

## 线程通信

这个和Vue那种父子组件通信不一样，也和通信工程那种链路什么什么的不一样，java的线程通信指的就是三个方法的使用。

wait()、notify()和notifyAll()。

- 这三个方法都是Object类的方法，而且都是finall修饰的。
- 这些方法都是只能在同步代码块/同步方法里使用，也就是说只能在锁里面使用。
- wait方法有异常，记得捕获一下。
- wait()方法会阻塞当前的运行的线程，并且释放钥匙。
- notify()方法会唤醒一个被wait的线程，次序按照线程优先级来。
- notifyAll()方法会唤醒所有被wait的线程。

接下来举一个例子。比如说我想让两个线程依次打印20到1，那肯定不能直接调用了，因为线程运行顺序都是随机的，所以可以考虑第一个线程打印完之后立刻wait()阻塞，等第二个线程打印完之后唤醒，然后第二个线程wait。这样就可以依次打印了。

```java
public static int num = 20;
public void run() {
	while (num > 0) {
		synchronized (this) {
      //先唤醒
			notify();
			if (num > 0) {
				System.out.println(Thread.currentThread().getName() + "："+ num );
				num--;
				try {
          //阻塞当前线程，并释放同步监视器。
					wait();
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}
	}
}
```

这个代码顺序如下：

1. 唤醒wait的线程，因为先开始没有wait的，所以没有效果。
2. 1号线程打印，调用wait()方法，被阻塞，释放key。
3. 2号线程拿着1号线程释放的key，进入run()。之后唤醒1号线程。
4. 2号线程打印完之后也阻塞，释放key。
5. 以此类推

![image-20200925151004593](img/image-20200925151004593.png)

因为sleep和wait比较像，所以最后对比一下。

- sleep使用位置没有限定，wait则只能在同步代码块或同步方法里面使用
- wait会释放同步监视器，sleep不会
- wait是Object的方法，而sleep是Thread的方法。

# 常用类

## Object类

### equals方法与==的区别

==若比较的是值类型，那么就比较值，并且允许自动类型转换。若是引用类型，那么就会比较两个对象的地址值是否相等。

```java
int a = 1;
float b = 1;
System.out.println(a==b);

lolis congYu = new lolis(13);
lolis congYu2 = new lolis(13);
System.out.println(congYu==congYu2); 
```

因为a和b的值是一样的，可以自动转换，所以答案为true。而congyu和congyu2的地址明显是两个不一样的，所以说会返回false。

那么用congyu的equals方法进行比较呢？

```java
lolis congYu = new lolis(13);
lolis congYu2 = new lolis(13);
System.out.println(congYu.equals(congYu2)); 
```

答案也是false，equals其实就是把==封装了一下而已。

```java
public boolean equals(Object obj) {
	return (this == obj);
}
```

这个是equals的源码，可以发现实际上就是在比较比较对象和当前对象的地址是否一样。

但是并不是所有的equals方法都这么鸡肋，比如说我下面这个代码。

```java
String god = new String("塞尔达传说");
String god2 = new String("塞尔达传说");
System.out.println(god.equals(god2)); 
```

同样是用equals但是这个却能返回true。这个很好理解，因为String子类重写了父类的equals方法。。这就好使了。

```java
public boolean equals(Object anObject) {
	if (this == anObject) {
		return true;
	}
	if (anObject instanceof String) {
		String aString = (String)anObject;
		if (!COMPACT_STRINGS || this.coder == aString.coder) {
				return StringLatin1.equals(value, aString.value);
		}
	}
	return false;
}
```

上面这个就是String种equals方法的源码，可以发现它核心代码就是`StringLatin1.equals(value, aString.value);`，而这个方法实际上是一个逐字比较的方法。

```java
public static boolean equals(byte[] value, byte[] other) {
  if (value.length == other.length) {
    for (int i = 0; i < value.length; i++) {
      if (value[i] != other[i]) {
        return false;
      }
    }
    return true;
  }
  return false;
}
```

所以说虽然Object类的equals方法和==完全一样，但是很多子类都会重写这个方法，所以用前看看源码比较好，不然用错会很尴尬。如果是你自己建的类，建议你也把equals方法重写了。

另外说一下重写equals的原则，因为equals是一个相等的运算，相等的对象一定满足等价条件，所以一定满足自反性，对称性和传递性。另外还要遵循算法的确定性，还有健壮性。

- 自反性：`a.equals(a)==true`
- 对称性：`a.equals(b)==true -> b.equals(a)==true`
- 传递性：`a.equals(b)==true ^ b.equals(c)==true  -> a.equals(c)==true`
- 传递的参数为null，应该返回false。`a.equals(null)==false`

### toString方法

这个东西我们平时用的，很多但是坑也很多。首先看一下OBject类直接调用toString的结果

```java
Object obj = new Object();
System.out.println(obj.toString()); 
System.out.println(obj); 
```

![image-20200921114104480](img/image-20200921114104480.png)

可以发现这两个玩意结果居然一模一样，也就是说实际上Object类中的toString方法就是打印当前对象的地址。下面放一下源码：

```java
public String toString() {
  return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

我们之前一直觉得obj就代表了对象的指针，实际上是不对的。`obj.toString()`才是打印指针的，而直接`System.out.println(obj); `实际上是间接调用了toString方法。下面是源码。

```java
public void println(String x) {
	if (getClass() == PrintStream.class) {
		writeln(String.valueOf(x));
	} else {
		synchronized (this) {
			print(x);
			newLine();
		}
	}
}

//String的valueOf方法
public static String valueOf(Object obj) {
        return (obj == null) ? "null" : obj.toString();
}
```

可以看到，实际上在打印对象的时候，最后还是调用了`obj.toString();`。

同样的，很多子类也重写了父类的toString方法。比如说String

```java
public String toString() {
  return this;
}
```

String直接返回了当前这个对象的实例，所以可以直接打印这个字符串。

## String类

### String的创建与初始化

#### 字面量初始化

```java
String name = "小丛雨";
```

#### 构造函数直接初始化

```java
String name = new String("芳乃酱");
```

#### 用数组初始化

```java
char[] girl = {'宁','宁'};
String name = new String(girl);
```

### String的储存结构

String是一个引用类型，但是为什么用字面量也能初始化呢？这时候数据是保存在堆空间还是栈空间呢？如果你看了String的源码，就会发现，String是通过`private final byte[] value;`来储存字符串的，明明是一个常量字符串，那为什么也可以直接对String的对象进行修改呢？这其实都是由String的储存特点决定的。

我们首先用一个例子抛砖引玉。

```java
String s1 = "꒰⑅•ᴗ•⑅꒱";
String s2 = "꒰⑅•ᴗ•⑅꒱";
System.out.println(s1==s2);
```

猜猜看结果会输出什么？为什么？

答案为true，实际上我是打算写一个css样式隐藏答案的，但是我发现typora好像不支持css代码的直接插入，，也不支持JavaScript的插入，，，唔，，问题不大，毕竟typora只是一个markdown编辑器，真要玩样式还得靠真正的浏览器。

好了有点偏题了，为什么会true呢？我们首先要明白String作为引用型数据，储存的一定是地址，而==运算符也比较的是地址值，之前刚刚说过。这就说明s1储存的地址等于s2的。

实际上String在用字面量初始化的时候，首先会在方法区的常量区里面创建字符串常量，之后把这个常量的地址返回给s1。这样s1就拿到了"꒰⑅•ᴗ•⑅꒱"的地址值。而s2在创建的时候，编译器发现常量区已经有了这个常量，就不会再创建新的了，直接把地址给了s2，这样s1和s2就拿到了一样的地址值。

一旦对s1或者s2的值进行修改，并不会直接修改常量池的内容，而是创建修改后的常量，再把地址传回去。所以你可以发现java中字符串不能用下标运算符直接修改字符串的值。`s1[0]='a'`，这种都是不行的，为什么呢？就是因为String的数据都在常量区，不能直接修改。只能通过创建新的常量来完成对数据的修改。
```java
String s1 = "꒰⑅•ᴗ•⑅꒱";
s1="(๑> ₃ <)";
```

就比如这个例子，s1原来指向"꒰⑅•ᴗ•⑅꒱"这个字符串常量的内存，之后编译器在常量区新建"(๑> ₃ <)"字符串常量，s1再次指向这个常量。也就是说自始至终常量区的数据是不允许被修改的。

字面量是这样创建的，其实用new也是一样的。

```java
String s1 = new String("꒰⑅•ᴗ•⑅꒱");
```

1. 在栈中创建s1变量
2. 在堆中创建一个String对象，把这个对象的指针赋给s1
3. 在常量区创建字符串常量"꒰⑅•ᴗ•⑅꒱"，然后把这个字符串常量的地址赋给String对象的value属性。

这样也完成了对String对象的创建。

### 字符串拼接原理

知道了字符串储存的原理，就可以来看看拼接的原理了。首先来看看下面的代码结果都是多少。

```java
String s1 = "Hello";
String s2 = "World";
final String s3 = "World";

String s4 = "HelloWorld";
String s5 = "Hello"+"World";
String s6 = s1+"World";
String s7 = "Hello"+s2;
String s8 = s1+s2;
String s9 = s7.intern();
String s10 = "Hello"+s3;

System.out.println(s4==s5);
System.out.println(s4==s6);
System.out.println(s4==s7);
System.out.println(s4==s8);
System.out.println(s4==s9);
System.out.println(s4==s10);
```

答案为：

- true
- false
- false
- false
- true
- true

实际上对于常量字符串的拼接，拼接之后会把结果保存在常量区，s4拼接之后刚好等于s5，所以就不再声明新的字符串常量了，此时s4和s5共用一个地址。

而如果拼接的一方出现了变量，那么就会把拼接的结果放在堆里面，所以地址不相同。最后如果调用字符串的intern()方法，那么编译器也会把字符串里面的内容放入常量区，然后返回这个指针。所以s9也拿到了"HelloWorld"的指针，所以s4==s9。

正如上面所说，s4的内容的放在常量池的，而s3本身就是常量，所以拼接之后也在常量池里面，所以s4==s10。

最后总结一下：

1. 常量与常量的拼接结果在常量池。且常量池中不会存在相同内容的常量。
2. 只要其中有一个是变量，结果就在堆中。
3. 如果调用intern()方法，字符串的值也会放入常量池中，并返回指针。
4. final修饰的常量也是储存在常量池的，拼接之后仍然在常量池。

### StringBuffer和StringBuilder

StringBuffer是可变长度的字符串，说是可变，其实也不可变，StringBuffer在初始化的时候直接给了16字节的长度，如果不够，那么动态扩容2倍。这样就构建了动态的字符串结构。具体操作会在数据结构讲到。同时，StringBuffer也是一个线程安全的类，下面是一部分源码，可以看到都用的是同步方法。

```java
public synchronized int length() {
	return count;
}

public synchronized int capacity() {
	return super.capacity();
}
```

StringBuilder和StringBuffer基本上一模一样，都是动态字符串。但是StringBuilder底层的方法本身同步方法，会导致线程安全。

String. stringBuffer.stringBuilder三者的异同：

- string:不可变的字符序列;底层使用byte[]存储
- StringBuffer:可变的字符序列;线程安全的，效率低;底层使用byte[]存储
- stringBuilder:可变的字符序列; jdk5.0新增的，线程不安全的，效率高;底层使用byte[]存

# 枚举

枚举类用于列举有限个常量。

## 枚举类的创建

### 自定义枚举类

枚举类对外暴露的都是静态公有属性，是通过本类构造函数提前创建的。并且对外不能暴露别的方法或属性。

```java
class Season {
	private final String seasonName;
	Season(String seasonName){
		this.seasonName = seasonName;
	}
	public static Season SPRING =  new Season("春");
	public static Season SUMMER =  new Season("夏");
	public static Season AUTUMN =  new Season("秋");
	public static Season WINTER =  new Season("冬");
}
```

### enum修饰的枚举类

上面的枚举类虽然很好用，但是写起来确实非常麻烦，为了节约程序员的头发，java提供了enum关键字，可以快速定义一个枚举类。

```java
enum Season {
	SPRING ("春"),
	SUMMER ("夏"),
	AUTUMN ("秋"),
	WINTER ("冬");
	private final String seasonName;
	private Season(String seasonName){
		this.seasonName = seasonName;
	}
}
```

这个写法和上面的等价，但是把那些重复的修饰符都省略了。

## 枚举类实现接口

如果想让枚举类实现接口，可以直接写。

```java
interface Info{
	void Show();
}

enum Season implements Info {
	SPRING ("春"),
	SUMMER ("夏"),
	AUTUMN ("秋"),
	WINTER ("冬");
	private final String seasonName;
	private Season(String seasonName){
		this.seasonName = seasonName;
	}
	public void Show() {
		System.out.println("我是季节枚举类");
	}
}
```

如果想让每个枚举对象有各自的方法，可以分别重写方法。

```java
interface Info {
	void Show();
}

enum Season implements Info {
	SPRING("春") {
		public void Show() {
			System.out.println("我是春天");
		}
	},
	SUMMER("夏") {
		public void Show() {
			System.out.println("我是夏天");
		}
	},
	AUTUMN("秋") {
		public void Show() {
			System.out.println("我是秋天");
		}
	},
	WINTER("冬") {
		public void Show() {
			System.out.println("我是冬天");
		}
	};

	private final String seasonName;

	private Season(String seasonName) {
		this.seasonName = seasonName;
	}
}
```

# 集合

![img](img/2243690-9cd9c896e0d512ed.gif)

集合就是进阶版数组，可以储存多个不同对象。但是数组在使用的时候，我们会遇到很多不能如愿的操作，下面是数组的一些缺点。

- 一旦初始化以后，其长度就不可修改。
- 数组中提供的方法非常有限，对于添加、删除、插入数据等操作，非常不便，同时效率不高。
- 数组没有现成的属性或方法获取数组中实际元素的个数
- 数组存储数据的特点:有序、可重复。对于无序、不可重复的需求，不能满足。

## Collection接口

下有两个实现类

- List
  - ArrayList
  - LinkedList
  - Vector
- Set
  - HashSet
  - LinkedHashSet
  - TreeSet

### 迭代器

使用iterator()方法可以获取Collection对象的迭代对象，之后可以用iterator.next()来遍历数据。

```java
Collection collection = new ArrayList();
collection.add(1);
collection.add(2);
//建立新的迭代器
Iterator iterator = collection.iterator();
while (iterator.hasNext()) {
  System.out.println(iterator.next());
}
```

除了遍历之外，也可以在遍历时删除数据

```java
//删除1
Collection collection = new ArrayList();
collection.add(1);
collection.add(2);
Iterator iterator = collection.iterator();
while (iterator.hasNext()) {
  Object object=iterator.next();
  if(object.equals(1)) {
    //remove不能连续使用，一个next一个remove
    iterator.remove();
  }
}
```

### forEach

集合也可以像数组一样使用forEach，但是内部调用的其实是迭代器。

```java
Collection collection = new ArrayList();
collection.add(1);
collection.add(2);
for (Object object : collection) {
  System.out.println(object);
}
```





### List接口

**有序,可重复**，类似于python里面的列表（实际上就是一回事）。本质是动态数组。

List接口下面有三个类，都是存储有序,可重复的数据。

- ArrayList是主要实现类，用数组实现。线程不安全，但是效率高
- LinkedList底层用链表实现
- Vector是很早就有的类的，用数组实现。线程安全，但是效率低

常用方法：

| 方法                            | 功能             |
| ------------------------------- | ---------------- |
| boolean add(E e);               | 增               |
| void add(int index, E element); | 插入             |
| E remove(int index);            | 删指定下标       |
| boolean remove(Object o);       | 删除指定元素     |
| E set(int index, E element);    | 改               |
| E get(int index);               | 查寻下标所在的值 |
| int size();                     | 长度             |

remove方法，如果传数值，默认为下标。

### Set接口

 **无序,唯一**，本质上是集合。无序并不是指随机存储，而是指在存放数据的时候，并不是按照插入的顺序储存的。

set接口下有三个实现类：

- HashSet：本质上是hashMap，在构造方法里面new了一个hashMap
- LinkedHashSet，是HashSet的子类，本质上还是无序储存，但是每个元素使用**双向链表**相互按照添加顺序来连接，来记录添加顺序。
- TreeSet：底层用红黑树储存，可以按照指定属性排序，所以不能添加不同类的对象

set没有定义新的方法，直接用collection的方法就行了。

#### set的无序性

set的数据是无序且不能重复的。

```java
Set set = new HashSet();
set.add(7);
set.add(5);
set.add(2);
set.add(3);
set.add(4);
set.add(6);
Iterator iterator= set.iterator();
while (iterator.hasNext()) {
	System.out.println(iterator.next());
}
//输出2 3 4 5 6 7
//可以看到结果并没有按照插入顺序输出
```

set的插入数据过程如下：

1. 首先要判断当前插入元素的hash值，然后计算出在数组中的位置
2. 判断计算出的位置是否已经有数据了。
3. 如果有说明hash值一样，此时调用equals方法，再次判断。如equals也一样说明数据重复，不可插入。
4. 如hash不一样或者equals不一样的话就插入。

所以说向Set中添加的数据，其所在的类一定要重写hashCode( )和equals()方法。

#### TreeSet

这个玩意里面是用红黑树实现的，主要就是用来排序，但是只能排序相同类的对象，否则无法比较。

但是编译器怎末知道你的排序规则的呢？这时候就需要定制排序规则。

编译器在判断对象是否相同的时候会调用compare方法，而不是equals方法。这时候就需要自定义Comparator的对象。

```java
public static void main(String[] args) {
	class Loli {
		int age;
		String name;

		public Loli(int a, String n) {
			age = a;
			name = n;
		}
		public void show() {
			System.out.println("我叫"+name+",今年"+age+"岁");
		}
	}

	Comparator comparator = new Comparator() {
		public int compare(Object o1, Object o2) {
			if (o1 instanceof Loli && o2 instanceof Loli) {
				Loli loli1 = (Loli) o1;
				Loli loli2 = (Loli) o2;
				return Integer.compare(loli1.age, loli2.age);
			} else {
				throw new RuntimeException("类型有错误");
			}
		}
	};

	Set set = new TreeSet<>(comparator);
	set.add(new Loli(13, "小玛琳"));
	set.add(new Loli(25, "塞尔达"));
	set.add(new Loli(3, "ココナツ"));
	set.add(new Loli(2, "チョコラ"));
	Iterator<Loli> iterator = set.iterator();
	while (iterator.hasNext()) {
		iterator.next().show();
	}
}
/*结果：
我叫チョコラ,今年2岁
我叫ココナツ,今年3岁
我叫小玛琳,今年13岁
我叫塞尔达,今年25岁
*/
```

可以看到结果会自动排序。



## Map接口

用于存储键值对，类似于python里面的字典，还有JavaScript里面的对象。

下有三个实现类

- HashMap：是Map的主要实现类;线程不安全的，但效率高;可以存储null的key和value
  - LinkedHashMap：在父类的基础上加入了指针链接结点。
- TreeMap：自带排序，底层仍然是红黑树
- Hashtable：是古老的实现类，线程安全，但效率低;不能存储null的key和vaLue。
  - Properties：常用来处理配置文件。key和vaLue都是string类型

键值对中，key不能重复，value可以。

# 泛型

# 反射

# 可视化

使用java swing

```java

```



# 常用操作

## 排序

以给萝莉排年龄为例

1. 实现Comparable接口
2. 重写compareTo方法
3. 把需要排序的数据放入List中
4. 使用java提供的排序方法
5. 打印结果/使用

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Sort {

	//1.实现Comparable接口
	class Loli implements Comparable<Loli>{
		int age;
		char oppai_size;//！平胸赛高！！！！！！！
		
		public Loli(int age) {
			this.age=age;
			this.oppai_size='A';
		}
		
		//2.重写compareTo方法
		@Override
		public int compareTo(Loli o) {
			//this.age-o.age 从小到大排序
			//o.age-this.age 从大到小排序
			return this.age-o.age;
		}
		
		//可选，重写toString方法
		@Override
		public String toString() {
			return "萝莉年龄="+age;
		}
	}
	
	public static void main(String[] args) {
		//3.把需要排序的数据放入List中
		List<Loli> loliList= new ArrayList<Loli>();
		loliList.add(new Sort().new Loli(10));
		loliList.add(new Sort().new Loli(14));
		loliList.add(new Sort().new Loli(12));
		loliList.add(new Sort().new Loli(18));
		loliList.add(new Sort().new Loli(400));
		
		//4.使用java提供的排序方法
		Collections.sort(loliList);
		
		//5.打印结果
		System.out.println(loliList);
	}
}
```

至于返回值的正负代表着什么需要自己来定义。

# 附录1-javadoc常用命令

| 标签                       | 说明                                                         | JDK 1\.1 doclet | 标准doclet   | 标签类型                            |
| -------------------------- | ------------------------------------------------------------ | --------------- | ------------ | ----------------------------------- |
| @author 作者               | 作者标识                                                     | √               | √            | 包、 类、接口                       |
| @version 版本号            | 版本号                                                       | √               | √            | 包、 类、接口                       |
| @param 参数名 描述         | 方法的入参名及描述信息，如入参有特别要求，可在此注释。       | √               | √            | 构造函数、 方法                     |
| @return 描述               | 对函数返回值的注释                                           | √               | √            | 方法                                |
| @deprecated 过期文本       | 标识随着程序版本的提升，当前API已经过期，仅为了保证兼容性依然存在，以此告之开发者不应再用这个API。 | √               | √            | 包、类、接口、值域、构造函数、 方法 |
| @throws异常类名            | 构造函数或方法所会抛出的异常。                               |                 | √            | 构造函数、 方法                     |
| @exception 异常类名        | 同@throws。                                                  | √               | √            | 构造函数、 方法                     |
| @see 引用                  | 查看相关内容，如类、方法、变量等。                           | √               | √            | 包、类、接口、值域、构造函数、 方法 |
| @since 描述文本            | 什么版本后就有了该方法/类。                                  | √               | √            | 包、类、接口、值域、构造函数、 方法 |
| \{@link包\.类\#成员 标签\} | 链接到某个特定的成员对应的文档中。                           |                 | √            | 包、类、接口、值域、构造函数、 方法 |
| \{@value\}                 | 当对常量进行注释时，如果想将其值包含在文档中，则通过该标签来引用常量的值。 |                 | √\(JDK1\.4\) | 静态值域                            |





# 附录2-java异常类

| 异常类型                       | 描述                             |
| ------------------------------ | -------------------------------- |
| NullpointerException           | 空指针异常                       |
| ArithmeticExecption            | 算数异常                         |
| NegativeArrayException         | 数组负下标异常                   |
| ArrayIndexOutOfBoundsException | 数组下标越界异常                 |
| FileNotFoundException          | 文件未找到异常                   |
| EOFException                   | 文件已结束异常                   |
| ClassCastException             | 类型强制转换异常                 |
| NegativeArraySizeException     | 创建一个大小为负数的数组错误异常 |
| OutOfMemoryException           | 内存不足错误                     |



# 附录3-String类常用方法

| 方法名                                                       | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| int length()                                                 | 返回字符串的长度:return value.Length                         |
| char charAt(int index)                                       | 返回某索引处的字符return value[index]                        |
| boolean isEmpty()                                            | 判断是否是空字符串: return value.Length == 0                 |
| String toLowercase()                                         | 使用默认语言环境，将String中的所有字符转换为小写             |
| string toUpperCase()                                         | 使用默认语言环境，将String中的所有字符转换为大写             |
| String trim()                                                | 返回字符串的副本，忽略前导空白和尾部空白                     |
| boolean equals(object obj)                                   | 比较字符串的内容是否相同                                     |
| boolean equalsIgnoreCase(String anotherString)               | 与equals方法类似，但忽略大小写                               |
| String concat(String str)                                    | 将指定字符串连接到此字符串的结尾。等价于用"+”                |
| int compareTo(String anotherString)                          | 比较两个字符串的大小                                         |
| String substring(int beginIndex)                             | 返回一个新的字符串，它是此字符串的从beginIndex开始截取       |
| String substring(int beginIndex，int endIndex)               | 返回一个新字符串，它是此字符串从[beginIndex,endIndex)左闭右开区间截取 |
| boolean endsWith(String suffix)                              | 测试此字符串是否以指定的后缀结束                             |
| boolean startsWith(String prefix)                            | 测试此字符串是否以指定的前缀开始                             |
| boolean startsWith(String prefix,int toffset)                | 测试此字符串从指定索引开始的子字符串是否以指定的前缀开始     |
| int indexOf(String str)                                      | 返回指定子字符串在此字符串中第一次出现处的索引               |
| int lastIndexOf(String str)                                  | 返回指定子字符串在此字符串中最右边出现处的索引               |
| boolean contains(CharSequence s)                             | 当且仅当此字符串包含指定的char值序列（字符串）时，返回true   |
| int indexOf(String str，int fromIndex)                       | 返回指定子字符串在此字符串中第一次出现处的索引               |
| int lastIndexOf(String str，int fromIndex)                   | 返回指定子字符串在此字符串中最后一次出现处的索引             |
| String replace(char oldChar,char newChar)                    | 返回一个新的字符串，它是通过用newChar替换此字符串中出现的所有oldChar得到的（替换的是字符） |
| String replace(CharSequence target，CharSequence replacement) | 使用指定的字面值替换序列替换此字符串所有匹配字面值目标序列的子字符串（替换的是字符串） |
| String replaceAll(String regex，String replacement)          | 使用给定的replacement替换此字符串所有匹配给定的正则表达式的子字符串 |
| String replaceFirst(String regex,String replacement)         | 使用给定的replacement替换此字符串匹配给定的正则表达式的第一个子字符串 |
| boolean matches(String regex)                                | 告知此字符串是否匹配给定的正则表达式。                       |
| String[] split(String regex)                                 | 根据给定正则表达式的匹配拆分此字符串。                       |
| String[] split(String regex, int limit)                      | 根据匹配给定的正则表达式来拆分此字符串，最多不超过limit个    |

注: indexo于和LastIndex0f方法如果未找到都是返回-1

# 附录4-Collection类常用方法

| 方法名                                     | 说明                                                         |
| ------------------------------------------ | ------------------------------------------------------------ |
| boolean add(E e);                          | 增加元素                                                     |
| boolean addAll(Collection<? extends E> c); | 把别的集合的元素全部拷贝到本集合里面                         |
| boolean contains(Object o);                | 判断集合中是否包含o，默认会调用equals方法，如果没有，需要自己手动重写 |
| boolean containsAll(Collection<?> c);      | c是否是当前集合的子集                                        |
| boolean remove(Object o);                  | 移除某个元素                                                 |
| boolean removeAll(Collection<?> c);        | 移除c集合与当前集合的交集                                    |
| boolean retainAll(Collection<?> c);        | 修改当前集合为：c与当前集合的交集                            |
| boolean equals(Object o);                  | 这个对象并不是直接实现了list或者set，但他必须是collection的一个子类。之后判断元素是否相等。 |
| int hashCode();                            | 计算hash值                                                   |
| Object[] toArray();                        | 将当前集合转化为数组                                         |
| Iterator<E> iterator();                    | 遍历集合                                                     |
|                                            |                                                              |
|                                            |                                                              |
|                                            |                                                              |


