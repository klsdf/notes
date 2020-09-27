# HTML基础

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

## 说明

本文不会收录所有的标签以及属性,只会挑选最为常用的和实用的,以便快速查找复习.

# 文档相关标签

## !DOCTYPE

!DOCTYPE是整个HTML最重要的标签,也是必写的标签,它表明了本HTML究竟采用哪一版html语言写的,因为除了HTML5之外还有XHTML,HTML 4.01 Strict,HTML 4.01 Transitional等等.不过现在一般都用的是HTML5.

`<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于` <html>` 标签之前。之后写上你需要的版本属性

```html
<!-- 声明HTML5 -->
<!DOCTYPE html>
```



## html

标志文档起点与终点

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

## link

一般常用于引用外部样式,或者JavaScript文件.

```html
<link rel="stylesheet" type="text/css" href="引用的路径" />
```

# 列表

## ul,li

无序列表

```html
<ul>
  <li>我</li>
  <li>是</li>
  <li>无序列表</li>
</ul>
```

<ul>
  <li>我</li>
  <li>是</li>
  <li>无序列表</li>
</ul>

## ol,li

顺序列表

```html
<ol>
  <li>我</li>
  <li>是</li>
  <li>有序列表</li>
</ol>
```
<ol>
  <li>我</li>
  <li>是</li>
  <li>有序列表</li>
</ol>

| 属性     | 值       | 描述                                                         |
| -------- | -------- | --------------------------------- |
| reversed | reversed | 规定列表顺序为降序。\(9,8,7\.\.\.\) |
| start    | 数字 | 规定有序列表的起始值。 |
| type     |1 A a I i  | 规定在列表中使用的标记类型。    |

## dl,dt,dd

```html
<dl>
  <dt>定义列表</dt>
  <dd>是专门写定义的列表,如下</dd>
  <dt>定义:</dt>
  <dd>我是内容</dd>
</dl>
```

<dl>
  <dt>定义列表</dt>
  <dd>是专门写定义的列表,如下</dd>
  <dt>定义:</dt>
  <dd>我是内容</dd>
</dl>

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

select定义选择列表（下拉列表）,option就是里面的选项，optgroup则是选项的分组

```html
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

# 表格

## table,td,tr,th

table用于定义表格,tr表示这是一行,td表示是一个元素.有几个tr就有几行,一个tr里面几个td就代表这行有几列.

要注意的是,第一行一般都是表格的头,所以用th修饰

```html
<table>
  <tr>
    <th>th表示表格头</td>
    <th>我也是表头</td>
    <th>我也是</td>
  </tr>
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

<table>
  <tr>
    <th>th表示表格头</td>
    <th>我也是表头</td>
    <th>我也是</td>
  </tr>
  <tr>
    <td>table表示一个表格，里面虽然啥都没有，但是可以放表格标签</td>
    <td>一个tr就用来表示一行表格</td>
    <td>td就表示每个单元格</td>
  </tr>
  <tr>
    <td>我是第2个tr，表示第二行</td>
  </tr>
</table>
**注意:!!!!!!表格默认是没有边框的,这个之所以有,是因为typora自动给我加了样式.**

table的属性:

<table>
	<tbody>
		<tr>
			<th style="width:20%;">属性</th>
			<th style="width:20%;">值</th>
			<th style="width:60%;">描述</th>
		</tr>
		<tr>
			<td>border</td>
			<td><i>pixels</i></td>
			<td>规定表格边框的宽度。</td>
		</tr>
		<tr>
			<td>cellpadding</td>
			<td>
				<ul>
					<li><i>pixels</i></li>
					<li><i>%</i></li>
				</ul>
			</td>
			<td>就是表格文字和格子边框的距离</td>
		</tr>
		<tr>
			<td>cellspacing</td>
			<td>
				<ul>
					<li><i>pixels</i></li>
					<li><i>%</i></li>
				</ul>
			</td>
			<td>每个单元格之间的距离</td>
		</tr>
		<tr>
			<td>frame</td>
			<td>
				<ul>
					<li>void</li>
					<li>above</li>
					<li>below</li>
					<li>hsides</li>
					<li>lhs</li>
					<li>rhs</li>
					<li>vsides</li>
					<li>box</li>
					<li>border</li>
				</ul>
			</td>
			<td>规定外侧边框的哪个部分是可见的。</td>
		</tr>
		<tr>
			<td>rules</td>
			<td>
				<ul>
					<li>none</li>
					<li>groups</li>
					<li>rows</li>
					<li>cols</li>
					<li>all</li>
				</ul>
			</td>
			<td>规定内侧边框的哪个部分是可见的。</td>
		</tr>
		<tr>
			<td>width</td>
			<td>
				<ul>
					<li><i>%</i></li>
					<li><i>pixels</i></li>
				</ul>
			</td>
			<td>规定表格的宽度。</td>
		</tr>
	</tbody>
</table>


td,th的属性

<table>
	<tbody>
		<tr>
			<th style="width:20%;">属性</th>
			<th style="width:20%;">值</th>
			<th style="width:60%;">描述</th>
		</tr>
		<tr>
			<td>align</td>
			<td>
				<ul>
					<li>left</li>
					<li>right</li>
					<li>center</li>
					<li>justify</li>
					<li>char</li>
				</ul>
			</td>
			<td>规定单元格内容的水平对齐方式。</td>
		</tr>
		<tr>
			<td>axis</td>
			<td><i>category_name</i></td>
			<td>对单元格进行分类。</td>
		</tr>
		<tr>
			<td>char</td>
			<td><i>character</i></td>
			<td>规定根据哪个字符来进行内容的对齐。</td>
		</tr>
		<tr>
			<td>charoff</td>
			<td><i>number</i></td>
			<td>规定对齐字符的偏移量。</td>
		</tr>
		<tr>
			<td>colspan</td>
			<td><i>number</i></td>
			<td>设置单元格可横跨的列数。</td>
		</tr>
		<tr>
			<td>headers</td>
			<td><i>idrefs</i></td>
			<td>由空格分隔的表头单元格 ID 列表，为数据单元格提供表头信息。</td>
		</tr>
		<tr>
			<td>rowspan</td>
			<td><i>number</i></td>
			<td>规定单元格可横跨的行数。</td>
		</tr>
		<tr>
			<td>scope</td>
			<td>
				<ul>
					<li>col</li>
					<li>colgroup</li>
					<li>row</li>
					<li>rowgroup</li>
				</ul>
			</td>
			<td>定义将表头数据与单元数据相关联的方法。</td>
		</tr>
		<tr>
			<td>valign</td>
			<td>
				<ul>
					<li>top</li>
					<li>middle</li>
					<li>bottom</li>
					<li>baseline</li>
				</ul>
			</td>
			<td>规定单元格内容的垂直排列方式。</td>
		</tr>
	</tbody>
</table>

## thead,tbody,tfoot

刚才那个表格其实不是完整版的,虽然也能用.但是实际开发中,能多严谨就要多严谨.

- thead用于表示表头
- tbody表示表格主题内容
- tfoot用于总结表的内容,当然你也随便写点啥
- **注意:这三个的顺序是thead,tfoot,tbody**

```html
<table>
	<thead>
		<tr>
			<th>妹子</th>
			<th>特征</th>
		</tr>
	</thead>
	<tfoot>
		<tr>
			<th>总体评价</th>
			<th>都是我老婆</th>
		</tr>
	</tfoot>
	<tbody>
		<tr>
			<td>牛顿</td>
			<td>金毛双马尾</td>
		</tr>
		<tr>
			<td>哈雷</td>
			<td>大胸软萌</td>
		</tr>
		<tr>
			<td>拉瓦锡</td>
			<td>腹黑</td>
		</tr>
	</tbody>
</table>
```



<table>
	<thead>
		<tr>
			<th>妹子</th>
			<th>特征</th>
		</tr>
	</thead>
	<tfoot>
		<tr>
			<th>总体评价</th>
			<th>都是我老婆</th>
		</tr>
	</tfoot>
	<tbody>
		<tr>
			<td>牛顿</td>
			<td>金毛双马尾</td>
		</tr>
		<tr>
			<td>哈雷</td>
			<td>大胸软萌</td>
		</tr>
		<tr>
			<td>拉瓦锡</td>
			<td>腹黑</td>
		</tr>
	</tbody>
</table>

## caption

表示表格的标题

```html
<table>
  <caption>牛顿与苹果树鉴赏表</caption>
	<thead>
		<tr>
			<th>妹子</th>
			<th>特征</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>牛顿</td>
			<td>金毛双马尾</td>
		</tr>
		<tr>
			<td>哈雷</td>
			<td>大胸软萌</td>
		</tr>
		<tr>
			<td>拉瓦锡</td>
			<td>腹黑</td>
		</tr>
	</tbody>
</table>
```

<table>
  <caption>牛顿与苹果树鉴赏表</caption>
	<thead>
		<tr>
			<th>妹子</th>
			<th>特征</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>牛顿</td>
			<td>金毛双马尾</td>
		</tr>
		<tr>
			<td>哈雷</td>
			<td>大胸软萌</td>
		</tr>
		<tr>
			<td>拉瓦锡</td>
			<td>腹黑</td>
		</tr>
	</tbody>
</table>



# 文本

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

<cite>cite语义表示引用，可以表示书名，电影什么的，表现为斜体</cite>

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

ruby用来表示<ruby>注<rt>zhù</rt></ruby><ruby>音<rt>yīn</rt></ruby>。
		ruby里面表示要注音的内容，rt里面表示拼音,若浏览器不支持，就需要用rp了，rp标签在 ruby 注释中使用，以定义不支持 ruby 元素的浏览器所显示的内容。
		我是<ruby>注音<rt><rp>(</rp>zhù yīn<rp>)</rp></rt></ruby>.

## ins

```html
<ins>这个表示下划线，填空题经常会看到</ins>
```

<ins>这个表示下划线，填空题经常会看到</ins>

## del

```html
<del>del里面的内容会被加入删除线，语义上就是删掉的内容</del>
```

<del>del里面的内容会被加入删除线，语义上就是删掉的内容</del>

## em

```html
<em>em语义上表示强调语气，表现为斜体</em>
```

<em>em语义上表示强调语气，表现为斜体</em>

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

<pre>
pre 元素可定义预格式化的文本。被包围在 pre 元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体。
说白了就是，pre里面怎么写，浏览器就怎么显示，因为一般浏览器会忽略多个回车和空格
int main()
{
	return 0;
}
但是注意标签不能放进去,有的不会显示
</pre>

## q

```html
<q>q标签表示短引用，一般语义上表示说话之类的，表现为在标签里面的内容，自动被加了双引号 </q>
<p>比如说，子曰:<q>知之为知之。</q></p>
<p>这个引号并不是HTML加的，所以鼠标也不能选中</p>
```

<q>q标签表示短引用，一般语义上表示说话之类的，表现为在标签里面的内容，自动被加了双引号 </q>

<p>比如说，子曰:<q>知之为知之。</q></p>
<p>这个引号并不是HTML加的，所以鼠标也不能选中</p>

## strong

```html
<strong>strong表示强烈强调，语气上非常激动，表现为黑体</strong>
```

<strong>strong表示强烈强调，语气上非常激动，表现为黑体</strong>

## sub

```html
sub表示 <sub>下标</sub>，经常用于x<sub>1</sub>之类的数学符号
```

sub表示 <sub>下标</sub>，经常用于x<sub>1</sub>之类的数学符号

## sup

```html
sup可以用来表示 <sup>上标</sup>,最常见就是y=x<sup>2</sup>
```

sup可以用来表示 <sup>上标</sup>,最常见就是y=x<sup>2</sup>



# HTML的全局属性

就是说所有html元素都具有这些属性,可以随便用.

| 属性            | 描述                                                   |
| --------------- | ------------------------------------------------------ |
| accesskey       | 规定激活元素的快捷键。                                 |
| class           | 规定元素的一个或多个类名（引用样式表中的类）。         |
| contenteditable | 规定元素内容是否可编辑。                               |
| contextmenu     | 规定元素的上下文菜单。上下文菜单在用户点击元素时显示。 |
| data\-\*        | 用于存储页面或应用程序的私有定制数据。                 |
| dir             | 规定元素中内容的文本方向。                             |
| draggable       | 规定元素是否可拖动。                                   |
| dropzone        | 规定在拖动被拖动数据时是否进行复制、移动或链接。       |
| hidden          | 规定元素仍未或不再相关。                               |
| id              | 规定元素的唯一 id。                                    |
| lang            | 规定元素内容的语言。                                   |
| spellcheck      | 规定是否对元素进行拼写和语法检查。                     |
| style           | 规定元素的行内 CSS 样式。                              |
| tabindex        | 规定元素的 tab 键次序。                                |
| title           | 规定有关元素的额外信息。                               |
| translate       | 规定是否应该翻译元素内容。                             |