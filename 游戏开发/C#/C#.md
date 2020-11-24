

# C#概述

## 基本结构

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace TEST
{
	class Program
	{
		static void Main(string[] args)
		{
      Console.WriteLine("Hello World!");
      Console.ReadKey();
		}
	}
}
```

## XML注释

 这是一个特殊的注释,跟java里面的一样,不仅仅可以用来为写源码的人提供提示,调用时也可以定制提示信息。

```c#
///<summary> 这是一个加法函数 </summary> 
/// <param name="a"> 参数</param>     
///<param name="b"> 也是参数</param>  
///<returns>返回a+b</returns>
public int Add(int a,int b) 
{
	return a+b;
}
```



## 专业术语

### 字段,属性

## 运算符

大部分运算符和别的语言都差不多,但是下面这些比较特殊,是需要强调的.

| 运算符   | 描述                                       | 示例 |
| :------- | :----------------------------------------- | ---- |
| typeof() | 返回是哪一种class                          |      |
| is       | 判断对象是否为某一个class的实例            |      |
| &        | 取地址，当然也有按位与的意思               |      |
| *        | 指针，接收地址,当然也有乘法的意思          |      |
| as       | 将左边的类型强制转换为右边，转不了返回null |      |

# 数据类型

## 值类型

### 基本值类型
|数据类型  |关键字|    值|
|--------|----|----------|
| 布尔类型  | bool | false,true |
|          | byte |            |
|          |      |            |
|          |      |            |

### 结构体

 看上去和c++的结构体一模一样，就是每个属性前面需要加一个访问权限,其实还是有很多不一样的地方

- 结构体不能有析构函数

- 不能为结构定义无参构造函数。无参构造函数(默认)是自动定义的，且不能被改变。

- 结构成员不能指定为 abstract、virtual 或 protected。

```C#
	struct Loli
	{
		public string name;
		public int age;
	};  
```

### 枚举

通过enum来声明。

```c#
enum Loli{傲娇,妹系,呆萌};
```
可以强制转换为int
```c#
int a =(int)Loli.傲娇;
```

## 引用类型

### 数组

#### 声明与初始化

```c#
	//用new初始化
	datatype[] arrayName = new datatype[num]{ };

	//直接初始化
	datatype[] arrayName = { 1,2,3 };
```



#### 多维数组

所谓多维数组其实就是维数相同的数组，比如二维数组，三维数组。

声明方法和一维数组一样，但是唯一的区别就是要用[,]来声明。

```c#
	//多维数组行列个数必须确定。
	int[,] a = {
		{1,2,3 },
		{4,5,6 },
	};
	//或者用new也可以声明
	int[,] a = new int[2,3]{{1,2,3}，{4,5,6}};
	//切记，不能写成int[2,3] a，不要被C语言迷惑了。
```

#### 交错数组

 第一个参数不能缺省，并且第二个不能加,因为这个玩意其实就是一个特殊的一维数组,只不过他每一个元素也是一个一维数组。

 所以你只能知道有多少个一维数组，但是不能指定每个一维数组里面有多少元素,所以每个元素都要初始化，并且只能用new

```c#
	int[][] a = new int[2][]{
		new int[]{1,2,3},
		new int[]{4,5} 
	};
```

#### foreach遍历

跟其他语言一样,foreach会遍历数组,i每次都会被赋值为数组的一个元素.

```c#
	int[] a=new int[3]{1,2,3}
	foreach (int i in a )
	{
		Console.WriteLine(i);
	}
```

结果会打印出1,2,3。这个i每次迭代会携带a[0],a[1],a[2]。并不是数组下标，而是元素本身。

当然了,在交错数组foreach的时候,要注意每次所携带的数据都是一个一维数组.

```c#
int[][] a = new int[2][] {
	new int[]{1,2,3},
	new int[]{4,5} 
};
foreach (int[] i in a)
	foreach (int j in i)
		Console.WriteLine(j);
```



### 字符串

## 其他类型

### 指针类型

### 可空类型

# 2020/6/15