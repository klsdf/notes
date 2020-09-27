# 基本样式

## 文字相关

### 文字颜色

```css
color: black;
```

颜色请参考我的颜色对照表

### 文本对齐

```css
text-align:center;
```

| 值      | 描述                                        |
| ------- | ------------------------------------------- |
| left    | 把文本排列到左边。                          |
| right   | 把文本排列到右边。                          |
| center  | 把文本排列到中间。                          |
| justify | 实现两端对齐文本效果。                      |
| inherit | 规定应该从父元素继承 text\-align 属性的值。 |

### 下划线

```css
text-decoration:none;
```

| 值            | 描述                                             |
| ------------- | ------------------------------------------------ |
| none          | 默认。定义标准的文本。                           |
| underline     | 定义文本下的一条线。                             |
| overline      | 定义文本上的一条线。                             |
| line\-through | 定义穿过文本下的一条线。                         |
| blink         | 定义闪烁的文本。                                 |
| inherit       | 规定应该从父元素继承 text\-decoration 属性的值。 |

### 行高

```css
line-height:20px;
```

| 值      | 描述                                                 |
| ------- | ---------------------------------------------------- |
| normal  | 默认。设置合理的行间距。                             |
| 某数字  | 设置数字，此数字会与当前的字体尺寸相乘来设置行间距。 |
| 某某px  | 设置固定的行间距。                                   |
| %       | 基于当前字体尺寸的百分比行间距。                     |
| inherit | 规定应该从父元素继承 line\-height 属性的值。         |

### 文字阴影

```css
text-shadow: 10px 5px 2px #FF0000;
```

| 参数       | 描述                                   |
| ---------- | -------------------------------------- |
| 第一个参数 | 必需。阴影离文字的水平距离。允许负值。 |
| 第二个参数 | 必需。阴影离文字的垂直距离。允许负值。 |
| 第三个参数 | 可选。代表这个阴影有多模糊。           |
| 第四个参数 | 可选。阴影的颜色。                     |

## 背景相关

### 背景颜色

```css
background-color: gray;
background-color: #bfc;
```

### 背景图片

```css
background-image:url("");
```

### 背景图片重复

```css
background-repeat:no-repeat;
```

| 值         | 描述                                                 |
| ---------- | ---------------------------------------------------- |
| repeat     | 默认。背景图像将在垂直方向和水平方向重复。           |
| repeat\-x  | 背景图像将在水平方向重复。                           |
| repeat\-y  | 背景图像将在垂直方向重复。                           |
| no\-repeat | 背景图像将仅显示一次。                               |
| inherit    | 规定应该从父元素继承 background\-repeat 属性的设置。 |


### 背景开始的位置

设置background-attachment:fixed;才能兼容 Firefox 和 Opera 浏览器

```css
background-attachment:fixed;
background-position:center;
```

<table>
  <tbody>
    <tr>
      <th>值</th>
      <th>描述</th>
    </tr>
    <tr>
      <td>
        <ul>
          <li>top left</li>
          <li>top center</li>
          <li>top right</li>
          <li>center left</li>
          <li>center center</li>
          <li>center right</li>
          <li>bottom left</li>
          <li>bottom center</li>
          <li>bottom right</li>
        </ul>
      </td>
      <td>
        <p>如果您仅规定了一个关键词，那么第二个值将是"center"。</p>
        <p>默认值：0% 0%。</p>
      </td>
    </tr>
    <tr>
      <td>x% y%</td>
      <td>
        <p>第一个值是水平位置，第二个值是垂直位置。</p>
        <p>左上角是 0% 0%。右下角是 100% 100%。</p>
        <p>如果您仅规定了一个值，另一个值将是 50%。</p>
      </td>
    </tr>
    <tr>
      <td>xpos ypos</td>
      <td>
        <p>第一个值是水平位置，第二个值是垂直位置。</p>
        <p>左上角是 0 0。单位是像素 (0px 0px) 或任何其他的 CSS 单位。</p>
        <p>如果您仅规定了一个值，另一个值将是50%。</p>
        <p>您可以混合使用 % 和 position 值。</p>
      </td>
    </tr>
  </tbody>
</table>
## 尺寸相关

### 宽度

```css
width:100px;
```



# 盒模型

## 概述

盒模型相关的样式包括:

- 内外边距
- 边框

CSS认为,每一个文档的元素都是一个盒子,这个盒子包括自身的大小,边框大小,内边距和外边距.如下图:

![CSS 框模型](img/ct_boxmodel.gif)

如果在浏览器(以chrome为例)里面用开发者工具查看,可以发现,实际上内外边距,外边距还有边框都是占地方的,

```css
p{
  border: #ADFF2F 10px solid;
  padding: 20px;
  margin: 30px;
  width: 50px;
  height: 50px;
}
```

![image-20200913130056030](img/image-20200913130056030.png)

![image-20200913130003875](img/image-20200913130003875.png)

这些样式的区别就在于,内边距是算在元素本身的大小里面的,啥意思呢,就比如你元素宽20px,内边距你两边各加10px,那么你这个元素整体就宽40px.边框也是一样的,但是外边距不会算在元素里面.

## 边框

### 概述

一个元素有上下左右四个边框(废话),css允许分别定义各个方向上边框的样式.比如说

```css
border-color:red green blue pink;
```

分别为上,右,下,左指定不同颜色.也就是从上开始,顺时针排列.

<p style="border-style:solid; border-color:red green blue pink;border-width:5px;width:100px;height:100px"></p>


```css
border-color:red green blue;
```

如果只写三个,那么第一个是上边框,第二个是左右边框,第三个是下边框.

<p style="border-style:solid; border-color:red green blue;border-width:5px;width:100px;height:100px"></p>

```css
border-color:red green;
```

只写两个的话就是上下边框,左右边框

<p style="border-style:solid; border-color:red green;border-width:5px;width:100px;height:100px"></p>

```
border-color:red;
```

一个的话肯定就是全部红喽;

<p style="border-style:solid; border-color:red;border-width:5px;width:100px;height:100px"></p>

这样分别指定样式的操作,在边框里面是通用的,也可以来指定宽度,表现等.如果不想这样隐式指定,也可以显示指定.

```css
border-top-width: 15px;
border-right-color: blue;
border-left-style: solid;
border-bottom-color: red;
```

像这样子,直接指定也是可以的.

**注意:!!!!!!!!!!!!!!只有把width,style和color都指定了之后才能正常显示边框,否则不会显示!!!!!!!!!!!!!!!!!!.**

### 边框表现

```css
border-style:solid;
```

| 值      | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| none    | 定义无边框。                                                 |
| hidden  | 与 "none" 相同。不过应用于表时除外，对于表，hidden 用于解决边框冲突。 |
| dotted  | 定义点状边框。在大多数浏览器中呈现为实线。                   |
| dashed  | 定义虚线。在大多数浏览器中呈现为实线。                       |
| solid   | 定义实线。                                                   |
| double  | 定义双线。双线的宽度等于 border\-width 的值。                |
| groove  | 定义 3D 凹槽边框。其效果取决于 border\-color 的值。          |
| ridge   | 定义 3D 垄状边框。其效果取决于 border\-color 的值。          |
| inset   | 定义 3D inset 边框。其效果取决于 border\-color 的值。        |
| outset  | 定义 3D outset 边框。其效果取决于 border\-color 的值。       |
| inherit | 规定应该从父元素继承边框样式。                               |

### 边框宽度

```css
border-width:20px;
```

| 值      | 描述                           |
| ------- | ------------------------------ |
| thin    | 定义细的边框。                 |
| medium  | 默认。定义中等的边框。         |
| thick   | 定义粗的边框。                 |
| 某某px  | 自定义宽度                     |
| inherit | 规定应该从父元素继承边框宽度。 |

### 边框颜色

```css
border-color:red green blue pink;
```

跟字体颜色一样,详情参考颜色表.

### 简写

因为边框想要生效必须指定三个属性,写起来确实很麻烦,为了增加程序员的寿命,HTML支持边框的简写

```css
border:5px solid red;
```

像这样,可以一次性设置三个属性.

# 选择器

## *选择器

就是全选的意思,选中html文档中所有的元素.

```css
*{
  margin:0;
  padding:0;
}
```

## 元素选择器

可以直接选择某一个标签,然后直接对HTML中所有这种标签进行批量编辑.

```css
p{
  color:red;
}
```

这个就是让所有p标签内部文字颜色变为红色.

## 类选择器

可以批量选择自定义的类,用于某一类特定的标签.

html:

```html
<ul>
  <li class="item">java</li>
  <li class="item">c#</li>
  <li class="item">sql</li>
  <li class="item">css</li>
</ul>
```

css:

```html
<style type="text/css">
	.item{
		color:blue
	}
</style>
```

一般类选择器选择的都是某一类标签,在需要添加这个类的标签前面加上`class`,后面可以指定想要的类,类名可以随便起.在css里面用点类名的办法,选择所有该类.

一般来说,类选择器都是批量选择很多该类的标签,比如说ul的列表,li有很多很多条,为每一个li单独设计样式岂不是累死了,所以可以给他们起一个类名item,批量添加这些li的样式.

## ID选择器

只能选择某一个特定的标签,一般只有一些特殊含义的标签才用起ID.还是刚才的例子.

html:

```html
<ul id="language-list">
  <li class="item">java</li>
  <li class="item">c#</li>
  <li class="item">sql</li>
  <li class="item">css</li>
</ul>
```

css:

```html
<style type="text/css">
	#language-list{
		color:blue
	}
</style>
```

ID选择器中,css用#加ID名就可以选中标签,一般一个网页里面这个语言列表可能就这么一个,所以比较特殊,可以用ID选择器来选中,直接操作这个标签.

## 伪类选择器

名字虽然很酷,其实没那么复杂,这个玩意可以来操作一些特殊的类,比如超链接的样式,输入框聚焦后的样式等等.写法就是在需要添加的元素后面冒号,然后加入想加入的伪类即可.

### 超链接相关

```css
a:link {color: #FF0000}		/* 未被访问的超链接 */
a:visited {color: #00FF00}	/* 已访问的链接 */
a:hover {color: #FF00FF}	/* 鼠标移动到超链接上的时候 */
a:active {color: #0000FF}	/* 鼠标点下去的一瞬间 */
```

### first-child

顾名思义,就是选择第一个子元素,但是这里面有很多坑,必须注意

先看html:

```HTML
<p><span>我是span</span>我是p</p>
<p><span>我是span</span>我是p</p>
```



- 选择所有p标签中,第一个p标签

```css
p:first-child{
  color: red;
} 
```

![image-20200913141409114](img/image-20200913141409114.png)

- 选择所有p标签内部第一个子元素

```css
p>:first-child {
	color: red;
}
```

![image-20200913141347709](img/image-20200913141347709.png)

### before和after

可以用这两个伪类,在某个元素前面或后面插入文本.用content来控制文本内容.

```css
p:before
{
	content:"我是before加的";
}
p:after
{
	content:"我是after加的";
}
```



## 并集选择器

如果你想同时给多个不同元素设置样式,可以用并集选择器

```css
body, h2, p, table, th, td, pre, strong, em {color:gray;}
```

像这样,彼此之间用逗号隔开,表示同时选中.

## 属性选择器

如果你想选择带某个属性的标签,可以用属性选择器.但是里面也有很多坑,需要注意.

- 指定某种属性

```css
a[href] {color:red;}
```

这个例子就是选择所有有href属性的a标签.也可以同时指定多个属性:

- 指定同时具有多种属性

```css
a[href][title] {color:red;}
```

这个就是选择同是有href和title属性的a标签

- 精确指定某个具体属性

```css
p[class="A B"] {color:red;}
```

选择某个有具体属性的标签,注意这个要求严格等于,也就是说你的class也必须是"A B",多一个空格都不行.这时候我们就可以使用下面的写法了.

- 含有某种属性

```css
p[class~="A"] {color: red;}
```

用这个~可以表示含有A的class,不用严格匹配.

属性选择器也支持三种正则语法:

- 包含某字符串的属性

```css
a[href*="dashepi.com"] {color: red;}
```

选择a标签的超链接中包含"dashepi.com"这个字符串的所有a标签

- 以某字符串开头的属性

```css
a[href^="www."] {color: red;}
```

选择href以"www."开头的a标签

- 以某字符串结尾的属性

```css
a[href$=".cn"] {color: red;}
```

选择href以".cn"结尾的a标签

# 定位与浮动

## 外边距重叠

## 高度塌陷

## 最终解决代码

```css
.clearfix::before,
.clearfix::after{
  content: "";
  display: table;
  clear: both;
}
```



# flex布局

子元素垂直水平居中

```css
display: flex;
align-items:center;  
justify-content:center;
```