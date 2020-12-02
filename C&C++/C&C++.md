# C/C++概述

## C/C++中的术语

### C11

指的是C11标准

# 输入/输出

## printf的输出顺序

printf在打印参数的时候是**从右往左**的，要特别注意。

```c
int main()
{
    int i = 1;
    printf_s("%d,%d",i,++i);
    return 0;
}
//2，2
```



## 输入缓冲区

在进行cin的时候，如果数据过多的话，输入缓冲区就会多出来很多完全没有用的数据，而且会对之后的数据造成干扰。这时候就可以把输入缓冲区进行清除。

```c++
char c;
while ((c = getchar()) != '\n');
```



# 数组

## 数组越界

首先看下面的代码。

```c++
#include<stdio.h>
int main()
{
	int i = 0;
	int a[10];
	for (i = 0; i <= 20; i++)
	{
		a[i] = 0;
		printf("i的地址是%p,a[i]的地址是%p\n",&i, &a[i]);
	}
	return 0;
}
```

这是一个平平无奇的越界。功能是把数组每一项都设为0。其实这个是有可能出现死循环的（其实就是一定，我试过了4个编译器都死循环了）**因为编译器可能会把i放在a数组的后面。**这就意味着，如果数组长度10，那么i的地址就在a[10]，或者a[11]之类的。具体的位置要根据编译器来决定。

这样的结构就导致了一个致命的问题。假如`&i=&a[10]`，**那么循环执行到a[10]的时候，就会把i的值重新置为0**。这就导致了i此时又变成了0，而再次运行到a[10]的时候，再次置为0。这样for循环将永远执行下去。

但是如果用c++的语法，在for循环内使用i，将不会导致循环，因为这样时，i的地址默认在数组之前，不会存在越界问题。

```c++
#include<stdio.h>
int main()
{
	int a[10];
	for (int i = 0; i <= 20; i++)
	{
		a[i] = 0;
		printf("i的地址是%p,a[i]的地址是%p\n",&i, &a[i]);
	}
	return 0;
}
```



## 指定初始器

c++允许在数组初始化时，用自身变量名来指定赋值。

```c++
int days[5] = {1,2,3,days[0]=4,5};
for (int i = 0; i < 5; i++)
{
  printf_s("days[%d]=%d\n",i,days[i]);
}
/*输出结果为
days[0]=4
days[1]=2
days[2]=3
days[3]=4
days[4]=5
*/
```

但是要注意，c++的执行顺序是顺序的，这就意味着，首先会把数组初始化为[1,2,3]，执行到`days[0]=4`之后，修改0的位置为4，然后再把自身的数据赋值为4，此时数组为[4,2,3,4]。

如果这个数字大于了自身下标，那么修改不会起效。如下

```c++
int days[5] = {1,2,3,days[4]=4,5};
for (int i = 0; i < 5; i++)
{
  printf_s("days[%d]=%d\n",i,days[i]);
}
/*输出结果为
days[0]=1
days[1]=2
days[2]=3
days[3]=4
days[4]=5
*/
```

此时，虽然在执行`day[4]=4`的时候把4号下标的数据改为了4，但是接下来又被5的数据重新覆盖了。

# 变量作用域

先看下面的代码

```c
int i = 1;

int main()
{
    int i = i;
    return 0;
}
```

main里面i的值将是多少？

答案是编译器会报错，外面的i作用域虽然是全局的，但是在函数作用域里面，会优先使用自己已经定义过的变量。

首先编译器会发现main中已经定义了i，然后初始化为i。之后编译器会去作用域链查找i的值，发现刚刚定义过了这个变量，之后就把刚刚那个定义的值（undefined）赋值给i。导致i的结果最后还是未定义。

# 函数

## 参数引用传递

尽量传引用，而不要直接值传递，因为引用传递的是指针，只有4字节，而值传递传递的数据可能会很多，影响速率。如果不希望修改原数据，只需要加const就行了。

## 函数返回值

void类型的函数，可以不写return，默认执行`return;`。

# 指针

指针就是地址，地址就是指针

## 指针常量和常量指针

这个其实不难的，主要是c++这个修饰符顺序没有定死，所以理解起来很困难，实际上按照真正的顺序去理解就好办了。

const修饰的变量就叫常量，那么const修饰的指针就叫指针常量。`int const a = 1;`，对const来说，a就是被修饰的东西，a整体就是常量，不能被修改。同样的，因为c++没有要求修饰符的顺序，所以`const int a = 1;`中，修饰的其实还是a，而不是int。想想也很简单，你修饰符总不能修饰修饰符吧？说到底还是修饰的变量。

话说回来，const修饰的东西就是常量，那么`int const *p;`，修饰的是`*p`，所以你这个`*p`就是常量，不可以修改。

这个就叫做**常量指针**。

就是说指向常量的指针，指针所指的东西不能被修改。

```c++
int a = 1;
int b = 2;
int const  *p_a = &a;
//*p_a = 2; //错误！！常量不可以被赋值
```

这里难点就在于int 和const是可以交换顺序的，所以`int const  *p_a = &a;`和`const int *p_a = &a;`实际上是等价的，因为int不能被修饰，所以const实际上还是在修饰`*p_a`。



接下来就是**指针常量**。

顾名思义们就是这个指针就是常量，不能乱指。

```c++
int a = 1;
int b = 2;
int* const p_a = &a;
//p_a = &b; // 错误！！常量不可以被赋值
```

const这次修饰的就是 `p_a`，所以`p_a`就是常量，不能被修改。 这个里面int* 和const不能交换顺序，所以说比较容易，因为一换的话，就变成了`const int *p_a = &a;`，就变成了常量指针。



所以区分这两个的方法就是看const修饰的到底是谁，修饰谁，谁是常量。但是这两个名字还是很难记啊。那么如何记住这两个名字呢？实际上我有一个技巧，const代表常量，*代表指针。`int const *p;`，这种先常量后指针的写法就叫常量指针，`int * const p;  `这种先指针后常量的就叫指针常量。

## 指针与引用

- 引用不可以为空，就是说初始化的时候就必须赋值，但是指针可以初始化为NULL
- 指针可以更改指向的对象，但是引用不可以指向新的变量。看来引用真的是老实人啊，指针太花心了。

# 枚举

## 使用与定义

```c++
enum class PROCESS_STATE {
    ready
};


STATE = PROCESS_STATE::ready;
```

# 命名空间

## 定义

程序设计里面经常就有变量名重复的问题，你跟其他人合作开发，你有一个a变量，人家说不定也有一个a变量，到时候一联合编译是不是就出错了，那怎么办？大佬们就想到一个方法，那就是把每个人的代码都放到自己的一个作用域里面，互不影响，这个作用域就叫做**命名空间**。

命名空间就是用`namespace`修饰的带名字的一个代码块，里面的数据不会影响到外界，这样子每个人的代码就独立开了。

```c++
namespace Loli {
	const char* name = "小丛雨";
	void show() {
		cout << "我叫" << name << endl;
	}
}
```



## 三种使用方式

- 使用`::`运算符

命名空间使用`::`运算符，可以直接访问到里面的数据，对于一些不常用的数据可以这样写，避免导入太多污染全局环境。

```c++
namespace Loli {
	const char* name = "小丛雨";
	void show() {
		cout << "我叫" << name << endl;
	}
}

int main()
{
	Loli::show();
	return 0;
}
```



- 使用`using`关键字

可以直接导入某个变量或函数，以后在全局空间可以直接使用，前面不用再写那一串东西了，比较方便。

```c++
namespace Loli {
	const char* name = "小丛雨";
	void show() {
		cout << "我叫" << name << endl;
	}
}
using Loli::show;

int main()
{
	show();
	return 0;
}
```

- `using namespace`命令

这个命令可以直接把命名空间所有数据都导出，虽然很方便，但是实际上已经起不到封装数据的作用了。我们常用的`using namespace std;`就是把std这个命名空间全部导入了，因为这个命名空间的数据使用频率非常高，所以可以直接导出，一般来说不建议这样写。

```c++
namespace Loli {
	const char* name = "小丛雨";
	void show() {
		cout << "我叫" << name << endl;
	}
}
using namespace Loli;

int main()
{
	show();
	return 0;
}
```

# 头文件

## 头文件的防卫式声明

```C++
#ifndef __COMPLEX__
#define __COMPLEX__
//代码
#endif 
```

## #include

自己写的头文件可以用“”来导入

```C++
#include "complex.h"
```

系统自带的头文件可以用<>来导入

```cpp
#include <iostream>
```



# 面向对象

## 类和对象的创建

```cpp
class Complex
{
private:
	int real;
	int img;
public:
	Complex(int real=0,int img=0) :real(real), img(img) {}
	void show(){ cout << real << "，" << img << endl; }
};
```

对象有两种创建方法。

- 直接创建

```cpp
const Complex complex(1,2);
complex.show();
```

- new创建

```cpp
Complex* complex = new Complex(1,2);
complex->show();
delete complex;
```



## 构造函数

构造函数的基本格式如下：

```cpp
class Complex
{
private:
	int real;
	int img;
public:
	Complex(int real=0,int img=0) :real(real), img(img) {
    cout<<"构造函数"<<endl;
  }
};
```

包括了参数列表，初始化列表和函数体。对于数据的初始化，请一定使用初始化列表，这样子看起来舒服，而且效率高。



构造函数可以直接调用，但是并不是所有编译器都会支持这个语法。

1. 直接调用

```
Complex::Complex(1,2);
```

2. 指针调用

可以对分配的内存进行初始化

```c++
void* memory = operator new(sizeof(Complex));//1.调用new运算符去分配内存
complex = static_cast<Complex*>(memory);//2.类型转换
complex->Complex::Complex(1, 2);//3.调用构造函数
```

## 构造函数的重载

构造函数可以重载，但是要注意，**无参构造函数**和**带了缺省参数的构造函数**不能共存。

```cpp
Complex(int real=0,int img=0) :real(real), img(img) {}
Complex(){}
```

在实例化时，`Complex* complex = new Complex();`之后编译器就会蒙蔽，因为这两个构造函数都满足调用条件，所以就会报错，说有多个多个构造函数可以被匹配。

## 空类的默认初始化

对于一个空类，编译器默认产生四个成员函数，

- 默认构造函数
- 析构函数
- 复制构造函数
- 重载赋值函数

## const

const的位置不同，功能也不同。

```cpp
void show() const{ cout << real << "，" << img << endl; }
```

这种写在成员函数右边的写法，就叫做**常量成员函数**。它代表这个函数不能修改对象的数据，只能读，不能写。

对于所有这种只读的函数，强烈建议都加上const，否则可能会出现下面的情况。

```cpp
class Complex
{
private:
	int real;
	int img;
public:
	Complex(int real=0,int img=0) :real(real), img(img) {}
	void show(){ cout << real << "，" << img << endl; }
};

int main() {
	const Complex complex(1,2);
	complex.show();//报错
	return 0;
}
```

看到了吗，首先const限定这个complex对象的数据不能被修改，之后调用show方法的时候，因为没有加const，所以代表show方法允许修改对象的数据，这时编译器就会报错，你对象说我的数据不能被修改，你的成员函数又说可以修改？这不就是矛盾了吗。如果show后面加上const就好了。

## struct和class

struct和class完全一样，唯一的区别就是class的默认访问权是private，而struct是public。

## 内联函数

用inline关键字声明的函数就是内联函数。用inline声明的函数，编译器**有可能**会把代码在编译时，直接把这个函数的内容插入到调用的地方，避免了重复调用的开销。

```c++
class Complex
{
private:
	int real;
	int img;
public:
	Complex() :real(0), img(0) {}
	inline void show() { cout << real << "，" << img << endl; }
};

int main() {
	Complex* complex = new Complex();
	complex->show();
	return 0;
}
```

上文中的show方法很短，所以调用时会直接变成**类似**下面的样子

```cpp
int main() {
	Complex* complex = new Complex();
	cout << real << "，" << img << endl;
	return 0;
}
```

跟宏很像，但是这个用起来更安全，也更简单。

## 访问级别

- public：公有
- protected：保护
- private：私有

## 友元函数

指的是可以访问类内私有数据的函数。

下面这个代码中，加法是成员函数，减法是友元函数。

```c++
#include <iostream>
using namespace std;

class Time
{
private:
    int time;
public:
    Time(int time = 0) {
        this->time = time;
    }
    int plus(int time) {
        this->time = (this->time + time) % 60;
        return this->time;
    }
    friend int sub(Time*, int);
    void show() {
        cout << "当前时间为" << this->time << endl;
    }
};

int sub(Time* t, int num)
{
    t->time = (t->time - num) % 60 > 0 ? (t->time - num) : 60 - (num - t->time) % 60;
    return t->time;
}

int main()
{
    Time* time = new Time();
    time->show();
    time->plus(129);
    time->show();
    sub(time, 120);
    time->show();
  	return 0;
}
```



**相同class的对象，互为友元**。

```cpp
class Complex
{
private:
	int real;
	int img;
public:
	Complex(int real=0,int img=0) :real(real), img(img) {}
	void show(){ cout << real << "，" << img << endl; }
	void visit(Complex complex) {
		cout << " " << complex.real << endl;
	}
};
```

可以看到，虽然这个visit函数没有声明为友元函数，但是依然可以访问其他对象的私有数据，这是因为同一个类下的对象互为友元。

# 模板

## 函数模板

如果函数变量或者返回值的类型不确定，就可以使用模板，如果用重载的话，种类太多，太累了。

```c++
template <typename T>
void bigger(T x1,T x2) {
	T temp = x1 > x2 ? x1 : x2;
	cout<<temp<<endl;
}

int main()
{
	int a1 = 3;
	int a2 = 4;
	bigger(a1, a2);

	float b1 = 10.3;
	float b2 = 3.4;
	bigger(b1, b2);
	return 0;
}
```



## 类模板 

跟函数模板差不多，但是在使用函数模板的时候一定要记住指定模板的类型。

```c++
template <typename T>
class Complex
{
private:
	T real;
	T img;
public:
	Complex() :real(0), img(0) {}
	void show() { cout << real << "，" << img << endl; }
};

int main() {
	Complex<int>* complex = new Complex<int>();
	complex->show();
	return 0;
}
```



# 堆栈与内存

## 栈中数据的生命周期

- 局部变量

对于局部变量来说，一旦离开作用域就会被析构。

```cpp
{
	Complex complex(1, 2);
}
//调用析构函数
```

- 静态局部变量

直到程序结束才会调用析构函数

```cpp
int main() {
	Complex complex(1, 2);
	return 0;
}
//调用析构函数
```

- 全局对象

和静态局部变量一样，也是程序结束才会调用析构函数

```cpp
Complex complex(1, 2);
int main() {
	return 0;
}
//调用析构函数
```



# STL

STL就是Standard Template Library的缩写，STL里面封装了贼多数据结构和算法，可以说是轮子大全了。再也不用重复造轮子了。

## vector

### 创建

```c++
#include <vector>
vector<数据类型> 变量名;
```

### 插入数据

```c++
vector<PCB*> pcb;
pcb.push_back(new PCB(0, 9, 0, 3));
```

### 删除数据

只能用erase方法删除数据，删除需要借助迭代器。

```c++
vector<PCB*>::iterator k = PCBList.begin();
PCBList.erase(k);
```

### 遍历

- for区间遍历

```c++
for (auto val : valList)
{
    cout << val << endl;
}
```

-  迭代器

```c++
vector<PCB*>::iterator it = PCBList.begin()+1;//可以用+1这种方法从第二个开始遍历
for (; it != PCBList.end(); ++it)
	cout << (*it)->ID << " ";
```

### 排序

首先必须自定义一个排序方法

```c++
static bool sortRules(const PCB* p1, const PCB* p2) {
	return p1->PRIORITY > p2->PRIORITY;
}
```

之后在需要的地方直接调用sort方法，并把排序方法传进去

```c++
sort(PCBList.begin(), PCBList.end(), PCB::sortRules);
```



# 常见错误

## VS中使用c语言函数

请在开头加上预编译

```c++
#define _CRT_SECURE_NO_WARNINGS
```

# 编程规范

