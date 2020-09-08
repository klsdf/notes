# 基础知识

## 发展史

## 基本结构

1. 文件名必须和public的类名一样也是test
2. 一个文件只能有一个public类

```java
//文件名必须是 test.java
public class test {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
```

## javadoc

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

# 数据类型

# 面向对象

## 封装

## 继承

## 多态

# 附录1   javadoc常用命令

<table>
	<tbody>
		<tr>
			<td>标签</td>
			<td>说明</td>
			<td>JDK 1.1 doclet</td>
			<td>标准doclet</td>
			<td>标签类型</td>
		</tr>
		<tr>
			<td>@author 作者</td>
			<td>作者标识</td>
			<td>√</td>
			<td>√</td>
			<td>包、 类、接口</td>
		</tr>
		<tr>
			<td>@version 版本号</td>
			<td>版本号</td>
			<td>√</td>
			<td>√</td>
			<td>包、 类、接口</td>
		</tr>
		<tr>
			<td>@param 参数名 描述</td>
			<td>方法的入参名及描述信息，如入参有特别要求，可在此注释。</td>
			<td>√</td>
			<td>√</td>
			<td>构造函数、 方法</td>
		</tr>
		<tr>
			<td>@return 描述</td>
			<td>对函数返回值的注释</td>
			<td>√</td>
			<td>√</td>
			<td>方法</td>
		</tr>
		<tr>
			<td>@deprecated 过期文本</td>
			<td>标识随着程序版本的提升，当前API已经过期，仅为了保证兼容性依然存在，以此告之开发者不应再用这个API。</td>
			<td>√</td>
			<td>√</td>
			<td>包、类、接口、值域、构造函数、 方法</td>
		</tr>
		<tr>
			<td>@throws异常类名</td>
			<td>构造函数或方法所会抛出的异常。</td>
			<td></td>
			<td>√</td>
			<td>构造函数、 方法</td>
		</tr>
		<tr>
			<td>@exception 异常类名</td>
			<td>同@throws。</td>
			<td>√</td>
			<td>√</td>
			<td>构造函数、 方法</td>
		</tr>
		<tr>
			<td>@see 引用</td>
			<td>查看相关内容，如类、方法、变量等。</td>
			<td>√</td>
			<td>√</td>
			<td>包、类、接口、值域、构造函数、 方法</td>
		</tr>
		<tr>
			<td>@since 描述文本</td>
			<td>什么版本后就有了该方法/类。</td>
			<td>√</td>
			<td>√</td>
			<td>包、类、接口、值域、构造函数、 方法</td>
		</tr>
		<tr>
			<td>{@link包.类#成员 标签}</td>
			<td>链接到某个特定的成员对应的文档中。</td>
			<td></td>
			<td>√</td>
			<td>包、类、接口、值域、构造函数、 方法</td>
		</tr>
		<tr>
			<td>{@value}</td>
			<td>当对常量进行注释时，如果想将其值包含在文档中，则通过该标签来引用常量的值。</td>
			<td></td>
			<td>√(JDK1.4)</td>
			<td>静态值域</td>
		</tr>
	</tbody>
</table>



