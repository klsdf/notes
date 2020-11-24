# 面板

## 创建

```java
JPanel 面板名 = new JPanel();
```



# 标签

## 创建

```java
JLabel input_1 = new JLabel("标签名");
```

# 文本输入框

## 创建

```java
JTextField 文本框 = new JTextField(文字长度);
```

## 常用方法

| 方法名            | 说明                 |
| ----------------- | -------------------- |
| setEnabled(false) | 是否禁用输入框       |
| setText("")       | 给文本框里面输入文本 |
|                   |                      |

# 按钮

## 创建

```java
JButton 按钮 = new JButton("按钮名");
```

## 事件监听

```java
按钮名.addActionListener(event -> {
		//代码
});
```



# 下拉框

## 创建

```java
String item[] =  new String[] {"+","-","*","/"};
JComboBox<String> 下拉框 = new JComboBox<String>(item);
```



