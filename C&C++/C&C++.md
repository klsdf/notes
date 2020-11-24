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

## 函数返回值

void类型的函数，可以不写return，默认执行`return;`。

# 指针

指针就是地址，地址就是指针

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



# 面向对象

## 类的创建

```cpp
class Test
{

};
```

## 空类的默认初始化

对于一个空类，编译器默认产生四个成员函数，

- 默认构造函数
- 析构函数
- 复制构造函数
- 重载赋值函数

## struct和class

struct和class完全一样，唯一的区别就是class的默认访问权是private，而struct是public。

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

