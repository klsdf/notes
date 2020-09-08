# HTML基础

## 发展史

## 基本结构

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>test</title>
	</head>
	<body>
    Hello World!
	</body>
</html>
```

## 专业术语

### 标签

HTML标签是HTML的基本组成,一般由一对<>组成,比如`<p>hello world</p>`对于只有一个<>的标签,我们叫单标签,单标签最后需要加`/`表示结束,比如`<img/>`

### 属性

每一个标签的开头,都可以加属性,比如`<a href=""></a>`,这个href就是属性,每一个元素都有一些自己独有的属性,而script 和style属性则是每个标签都有的.

### 文档

HTML文档从`<html>`开始,在`</html>`结束,这里面包裹的内容就是HTML文档,文档头由`<head>`定义,而文档主体由`<body>`定义.



# 文档相关标签

## !DOCTYPE

!DOCTYPE是整个HTML最重要的标签,也是必写的标签,它表明了本HTML究竟采用哪一版html语言写的,因为除了HTML5之外还有XHTML,HTML 4.01 Strict,HTML 4.01 Transitional等等.不过现在一般都用的是HTML5.

`<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于` <html>` 标签之前。之后写上你需要的版本属性

```html
<!-- 声明HTML5 -->
<!DOCTYPE html>
```



## html

## meta

mtea可以提供有关页面的元信息,就是说,可以给搜索引擎提供一个简历,以确保被搜索到.

# 基础标签

## p

定义段落

```html
<p>块级元素的标签</p>
```

## span

```html
<span>行内元素的标签</span>
```

## hr

```html
<p>
	hr在换行后加水平线<hr/>就像这样
</p>
```

## br

```html
<p>
	br仅仅表示换行<br>就像这样
</p>
```

## 注释

```html
<!-- 我是注释 -->
```



# 链接

## a

```html
<a href="超链接连接的网址">a标签是一个超链接</a>
```

# 列表

## ul,li

```html
<ul>
  <li>我</li>
  <li>是</li>
  <li>无序列表</li>
</ul>
```



## ol,li

顺序列表

```html
<ol>
  <li>我</li>
  <li>是</li>
  <li>有序列表</li>
</ol>
```

指定序号起点

```html
<ol start="50">
  <li>而且</li>
  <li>可以</li>
  <li>指定序号</li>
</ol>
```

倒序表示

```html
<ol reversed="reversed">
  <li>我</li>
  <li>是</li>
  <li>倒序列表</li>
</ol>
```






## dl,dt,dd

```html
<dl>
  <dt>定义列表</dt>
  <dd>是专门写定义的列表,如下</dd>
  <dt>定义:</dt>
  <dd>我是内容</dd>
</dl>
```



# 表单

## form

```html
<form action="/demo/demo_form.asp">
	form表示一个表单，里面本身啥都没有，但是可以放各种表单的标签
	<br>
	我是一个input：
	<input type="text" name="firstname" value="我是一个text input">
	<br>
	<button type="button">我是一个button</button>
</form> 
```



## fieldset,legend

```html
<form>
  <fieldset>
	<legend>我是legend，我是这个表单的边框信息</legend>
	周围这一圈框框就是fieldset控制的
	<br>
	输入框：<input type="text" />
  </fieldset>
</form>
```



## button

```html
<button type="button">button就是一个按钮</button>
```

## select,optgroup,option 

```html
select定义选择列表（下拉列表）,option就是里面的选项，optgroup则是选项的分组<br>

<select>
  <optgroup label="我是optgroup,我是第一组选项">
	<option value ="被送去服务器的值">option1</option>
	<option>选项2</option>
  </optgroup>

  <optgroup label="我也是optgroup,我是第二组选项">
	<option>option3</option>
	<option>选项4</option>
  </optgroup>
</select>
```



# 表格

## table,td,tr

```html
<table border="1">
  <tr>
    <td>table表示一个表格，里面虽然啥都没有，但是可以放表格标签</td>
    <td>一个tr就用来表示一行表格</td>
    <td>td就表示每个单元格</td>
  </tr>
  <tr>
    <td>我是第2个tr，表示第二行</td>
  </tr>
</table>
```



# 文本标签

## abbr

用于定义缩写,并且鼠标滞留时还可以有提示

```html
镜5莲华下海了,<abbr title="爷的青春结束了">爷青结</abbr>.
```

镜5莲华下海了,<abbr title="爷的青春结束了">爷青结</abbr>.



## blockquote

```html
blockquote是一个长引用，
<blockquote>
  它里面的内容会根据编译器自动排版，表示一个段落的引用
</blockquote>
```

blockquote是一个长引用，
<blockquote>
  它里面的内容会根据编译器自动排版，表示一个段落的引用
</blockquote>

## cite

```html
<cite>cite语义表示引用，可以表示书名，电影什么的，表现为斜体</cite>
```



## ruby，rt，rb

```html
ruby用来表示
<ruby>注<rt>zhù</rt></ruby>
<ruby>音<rt>yīn</rt></ruby>。
ruby里面表示要注音的内容，rt里面表示拼音<br>
若浏览器不支持，就需要用rp了，<br>
rp标签在 ruby 注释中使用，以定义不支持 ruby 元素的浏览器所显示的内容。<br>
我是<ruby>注音<rt><rp>(</rp>zhù yīn<rp>)</rp></rt></ruby>
```



## ins

```html
<ins>这个表示下划线，填空题经常会看到</ins>
```



## del

```html
<del>del里面的内容会被加入删除线，语义上就是删掉的内容</del>
```



## em

```html
<em>em语义上表示强调语气，表现为斜体</em>
```



## pre

```html
<pre>
pre 元素可定义预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体。
说白了就是，pre里面怎么写，浏览器就怎么显示，因为一般浏览器会忽略多个回车和空格
int main()
{
	return 0;
}
但是注意标签不能放进去,有的不会显示
</pre>
```



## q

```html
<q>q标签表示短引用，一般语义上表示说话之类的，表现为在标签里面的内容，自动被加了双引号 </q>
<p>比如说，子曰<q>知之为知之。</q></p>
<p>这个引号并不是HTML加的，所以鼠标也不能选中</p>
```



## strong

```html
<p>
	<strong>strong表示强烈强调，语气上非常激动，表现为黑体</strong>
</p>
```



## sub

```html
<p>
  sub表示 <sub>下标</sub>，经常用于x<sub>1</sub>之类的数学符号
</p>
```



## sup

```html
<p>
  sup可以用来表示 <sup>上标</sup>,最常见就是y=x<sup>2</sup>
</p>
```





