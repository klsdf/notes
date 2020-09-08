# 样式大全

## 文字相关

### 文字颜色

```css
color: black;
```

颜色请参考我的颜色对照表

### 下划线

```css
text-decoration:none
```

<table>
  <tbody>
 		<tr>
      <th>值</th>
      <th>描述</th>
    </tr>
    <tr>
      <td>none</td>
      <td>默认。定义标准的文本。</td>
    </tr>
    <tr>
      <td>underline</td>
      <td>定义文本下的一条线。</td>
    </tr>
    <tr>
      <td>overline</td>
      <td>定义文本上的一条线。</td>
    </tr>
    <tr>
      <td>line-through</td>
      <td>定义穿过文本下的一条线。</td>
    </tr>
    <tr>
      <td>blink</td>
      <td>定义闪烁的文本。</td>
    </tr>
    <tr>
      <td>inherit</td>
      <td>规定应该从父元素继承 text-decoration 属性的值。</td>
    </tr>
	</tbody>
</table>

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

<table>
  <tbody>
    <tr>
      <th>值</th>
      <th>描述</th>
    </tr>
    <tr>
      <td>repeat</td>
      <td>默认。背景图像将在垂直方向和水平方向重复。</td>
    </tr>
    <tr>
      <td>repeat-x</td>
      <td>背景图像将在水平方向重复。</td>
    </tr>
    <tr>
      <td>repeat-y</td>
      <td>背景图像将在垂直方向重复。</td>
    </tr>
    <tr>
      <td>no-repeat</td>
      <td>背景图像将仅显示一次。</td>
    </tr>
    <tr>
      <td>inherit</td>
      <td>规定应该从父元素继承 background-repeat 属性的设置。</td>
    </tr>
  </tbody>
</table>

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



# 盒模型

# 选择器

# 定位与浮动

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