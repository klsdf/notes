# 基础

## Python的运行

Python源代码都是`.py`文件，在终端直接输入`python xxx.py`就可以调用python的解释器。

## 注释

```python
#python用井号当单行注释
```

```python
"""
多行注释用三个单引号或者双引号开启
"""
```



## 基础语法

- 没有分号
- python是弱类型语言，不用声明变量类型
- 严格要求回车与空格
- 不提供num与string的自动类型转换，不会自己把num和string解包装包。

## 基础结构

```python
print("hello world")
myName=input()
print("hello!"+myName)
```



# 数据类型

## 全局变量

用 global修饰的变量会变成全局变量 

## None值

python用None表示null

# 流程控制

## if语句

```python
gender='男'
if gender=='男':
  print("大叔")
elif gender=='女':
  print("萝莉")
else:
  print("性别有问题")
```



## while语句

continue用于中断此次循环，返回开头。**每个while循环和for循环的结尾会隐式加上continue，以便再次执行。**

例：打印除了6以外其他的数

```python
num=0
while num!=10:
  if num==6:
    num=num+1
    continue
  print(num)
  num=num+1
```

break用于中断整个循环

例：打印6以前的数

```python
num=0
while num!=10:
  if num==6:
    break
  print(num)
  num=num+1
```



## for循环

主要就是用的range函数，range函数有三个重载，每个重载多一个参数

1. 一个参数时，表示迭代的次数。（从0开始）

```python
for i in range(10):
  print(i)
```

2. 两个参数时，代表打印范围

```python
for i in range(10,20):
  print(i)
```

3. 三个参数时，前两个代表范围，后面一个代表步长，也就是每隔几个打印一次

```python
for i in range(10,20,2):
  print(i)
```

# 函数

如果没有返回值，编译器会默认在结尾加上`return None`

```python
def add(a,b):
  return a+b
c=add(2,5)
print(c)
```

# 格式输出

## 不换行打印

用end关键字来指定下一行不换行

```python
print("hello ",end="")
print("world")
```

## 多值打印的分隔符

如果print传入多个参数，那么会默认用空格作为分隔符

```python
print("hello","world")
#hello world
```

用sep可以修改分隔符

```python
print("hello","world",sep=",")
#hello,world
```

## pprint模块

pprint模块自带很棒的格式输出。

```python
import pprint
num = {2,3,5,1,5,6,8,1,7,8,2,3,6}
pprint.pprint(num)
#{1, 2, 3, 5, 6, 7, 8}
```

可以看到它会对字典自动排序和去重

# 列表

就是数组

## 负数下标

python允许下标为负数，此时循环到末尾

```python
a=[1,2,3,4,5,6,7]
print(a[-1])
```

打印7

## 数组切片

python提供了切割数组的功能。中间用冒号连接，表示一个左闭右开区间。

```python
a=[1,2,3,4,5,6,7]
print(a[1:2])
#答案
#[2]
```

表示从下标1开始，打印到下标2之前。

## 列表长度

用len()函数也可以展示数组长度

```python
a=[1,2,3]
print(len(a))
```



## 列表的连接与复制

直接用运算符就可以了，无敌。

```python
a=[1,2,3]
b=[4,5,6]+a
c=a*3
print(b)
print(c)
#答案
#[4, 5, 6, 1, 2, 3]
#[1, 2, 3, 1, 2, 3, 1, 2, 3]
```

## 删除元素

用del语句

```python
a=[1,2,3]
del a[1]
print(a)
#[1,3]
```

## in与not in

用in与not in运算符可以判断一个数是否在数组中。

```python
a=[1,2,3]
print(2 in a)
print(4 not in a)
#答案
#True
#True
```

## 多重赋值

python允许用数组多重赋值。md，有一说一，实在是太强大的，怪不得现在这么多高中生都会编程了。不过到后面都一样难。

```python
asuna=["亚丝娜","172"]
name,height=asuna
print(name+"身高为"+height)
#结果
#亚丝娜身高为172
```




## 常用方法

| 方法                | 功能                             |
| ------------------- | -------------------------------- |
| .index(data)        | 返回data所在的下标，没有则会异常 |
| .append(data)       | 在数组末尾添加元素               |
| .insert(index,data) | 指定位置添加元素                 |
| .remove(data)       | 删除data元素，返回值为data       |
| .sort()             | 排序                             |
| .reverse()          | 转置数组                         |

# 元组

## 定义与使用

元组和列表的区别如下：

1. 元组是不可变的。
2. 用圆括号来定义。

```python
asuna=("亚丝娜","172")
asuna[0]=1
#会报错，因为元组的值不能被修改
```

## 与列表的相互转换

1. 元组转列表，使用list()方法

```python
asuna=("亚丝娜","172")
print(list(asuna))
```

2. 列表转元组，使用tuple()方法

```python
asuna=["亚丝娜","172"]
print(tuple(asuna))
```

# 字典

## 定义与使用

就是对象，和JavaScript的对象一模一样，键值对的字面量来定义字典。字典的无序的，不能用a[0]，这种方式访问，只能用键名直接访问。

```python
asuna={"name":"asuna","age":18}
print(asuna["name"])
```

## 遍历字典的三个方法

1. 遍历键

其中这个.keys()可以省略，默认就是遍历建

```python
asuna={"name":"asuna","age":18}
for item in asuna.keys():
  print(item)
#name
#age
```

2. 遍历值

```python
asuna={"name":"asuna","age":18}
for item in asuna.values():
  print(item)
#asuna
#18
```

3. 遍历键值对

```python
asuna={"name":"asuna","age":18}
for item in asuna.items():
  print(item)
#('name', 'asuna')
#('age', 18)
```

## get()方法

访问字典中不存在的数据会报错。但是python提供了get()方法，可以允许你自定义，当访问的键不存在时，返回什么值。很像MySQL里面那个IFNULL `SELECT IFNULL(loli_name,0)  FROM lolis;`，也是保护数据的。防止查询到非法数据。

```python
asuna={"名字":"亚丝娜","年龄":18}
print(asuna.get("名字","桐人"))
print(asuna.get("胸围","A"))
#亚丝娜
#A
```

这里面就是说，如果找到了名字的键就打印asuna的值，没有就打印桐人。同样的，如果找到了胸围的键就打印，否则就返回A。

## setdefault()方法

这个方法可以在字典中添加新的键值对。`setdefault(键,值)`。如果所添加的键在原字典中没有，那么就会增加。如果已经存在，那么不变。

```python
asuna={"名字":"亚丝娜","年龄":18}
asuna.setdefault("胸围","B")
asuna.setdefault("胸围","C")
print(asuna)
#{'名字': '亚丝娜', '年龄': 18, '胸围': 'B'}
```

# 字符串

## 原始字符串

如果想在字符串里面使用反斜线一般都是使用转义字符，但是在python里面也可以使用原始字符串，它会保留这些特殊的语法。

在字符串引号前面加上r就可以变成原始字符串了。

```python
str=r"\1\23\\\3"
print(str)
#\1\23\\\3
```

## 多行字符串

用于打印多行字符串，编译器会保留回车,引号等特殊字符。用三个单引号或者双引号开启。顺带一提，markdown的代码块也是用三个单引号开启的。

```python
str='''
#include<iostream>
using namespace std;
int main()
{
  cout<<"hello world!";
  return 0;
}
'''
print(str)
```

一般也用于多行注释。

# 常用功能

## 强行结束程序

```python
import sys
while True:
  print(123)
  sys.exit()
```

## 随机数

```python
import random
for i in range(5):
  print(random.randint(1,10))
```



# 常用函数

## 字符串相关

| 函数名  | 功能                      | 例子                 |
| ------- | ------------------------- | -------------------- |
| print() | 打印字符串                | print("hello world") |
| input() | 接收用户输入的字符串      | myName=input()       |
| len()   | 返回字符串长度            | len("hello")         |
| str()   | 转换为string类型          | str(0721)            |
| int()   | 转换为int类型，会数据丢失 | int("0721")          |
| float() | 转换为float类型           | float(0721)          |
|         |                           |                      |
|         |                           |                      |
|         |                           |                      |

