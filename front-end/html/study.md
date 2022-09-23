# HTML5的学习笔记

## W3C的历史

最开始的浏览器，对页面的渲染没有统一的标准，使得相同的代码，在不同的浏览器渲染结果不同，W3C（World Wide Web Consortium，万维网联盟）为制作标准，使得页面渲染在不同浏览器保持一致而诞生。

## W3C规范包括哪些？

W3C规范是一系列标准的集合，包含了三个部分：

1. 网页的结构（如：HTML）
2. 网页的表现（如：CSS）
3. 网页的行为（如：JavaScript）

## HTML的全名

Hypertext Markup Language，超文本标记语言。

## 换行符号和空格的注意事项

在网页中默认会忽略换行符，将多个空格合并为一个空格。

```html
  a
  b
  c

<!-- 渲染成：a b c -->
```

## 注释的写法

注释不能嵌套使用。

```html
<!-- 写法一，单行注释 -->
<!--
  写法二，多行注释
-->
```

## 文档类型声明的注意事项

- 由于W3C标准的不断迭代，出现不同的高低版本，因此需要对文档使用的规范进行声明，如果声明会按照怪癖模式对页面进行渲染。怪癖模式在不同浏览器的解析不同，是指按照低版本（很老的解析模式）来对页面进行解析渲染，主要会影响CSS（Cascading Style Sheet，层叠样式表）的解析。

- 文档类型声明不属于HTML标签。
- 文档类型声明必须写在网页文档开头。
```html
<!DOCTYPE html>
<html>
  <!--
    网页内容
  -->
</html>
```

## 字符编码问题

每个国家的语言在计算机中都是以二进制存储，而如何让每个语言符号都能找到对应的一段二进制位数据？字符编码标准因此诞生。而不同国家有不同的字符编码标准，不同国家之间需要互相交流，因此需要一个包含所有国家语言的字符编码标准，而Unicode编码标准因此诞生。

[详细见此](https://dailc.github.io/2017/05/17/severalCommonlyCharEncoding.html)

## VSCode插件-liveServer插件

快速搭建一个服务器，有热更新功能。****

## 字符实体

一些特殊的符号在文档中不能直接书写表示，比如`<`、`>`、`@`，需要用转义符号对其进行表示，这些转义符号较字符实体。

[字符实体表](https://www.w3school.com.cn/html/html_entities.asp)

## meta标签的常用属性

`name/content`、`http-equiv/content`和`charset`

## meta.name.description的作用

用作浏览器搜索结果中内容的描述，也即每条搜索结果下面的一小段文字。

## 语义化标签的注意事项

语义化标签是指具有特殊含义的标签，使文档具有更高的维护性和阅读性。常见的语义化标签有：`title`、`h1`、`p`、`em`、`strong`、`blockquote`、`q`、`header`、`nav`、`main`、`article`、`section`、`aside`。

![语义化标签的含义](./images/语义化标签的含义.png)

[查看有哪些语义化标签](https://www.w3school.com.cn/html/html5_semantic_elements.asp)

## 无序列表、有序列表和定义列表的使用

```html
<!-- 无序列表ul（unorder list）和li（list item）-->
<ul>
  <li>苹果</li>
  <li>葡萄<li>
</ul>

<!-- 有序列表ul（order list）和li（list item） -->
<ol>
  <li>苹果</li>
  <li>葡萄<li>
</ol>

<!-- 定义列表（definition list）、dt和dd -->
<dl>
  <dt>苹果的优点</dt>
  <dd>优点1</dd>
  <dd>优点2</dd>
  <dd>优点3</dd>
</dl>

```

## 超链接的注意事项

### 使用方式

- 跳转页面

`<a href='https://baidu.com'>百度</a>`

- 下载文件

`<a href='https://download-path/target.png' download>下载图片</a>`

- 锚链接

```html
<!-- 使用id定位，适用于任何标签 -->
<a href="#apple">跳转到苹果</a>
...
<h1 id="apple">苹果</h1>
<p>...</p>

<!-- 使用name定位，适用于任何标签 -->
<a href="#apple">跳转到苹果</a>
...
<a name="apple" href="https://www.apple.com">苹果</a>
```

### 常用属性

1. href，指定跳转地址。
2. target，指定跳转的方式。
3. download，指定超链接用于下载文件。

### target属性的值

1. _self，在本页跳转。
2. _blank，新建页面跳转。
3. _parent，在父窗口打开。
4. _top，在顶层窗口打开。

## 内联元素、块状元素和内联块状元素的区别

- 内联元素，不独占一行，不可以设置宽高、边框、上下外边距和上下内边距。
- 块状元素，独占一行，可以设置宽高、边框、外边距和内边距。
- 内联块状元素，不独占一行，但是可以设置宽高、边框、外编剧和内边距。

## 可替换元素和不可替换元素的区别

- 可替换元素指用于表示视频、音频、图片和内联框架这些需要在加载后后才知道具体规格的资源的标签元素。
- 不可替换元素指代除可替换元素的其他一般的标签元素。

## 常见的图片格式的优缺点

- `jpg`又名`jpeg`，支持的颜色丰富，不支持图片透明和动图。
- `png`，支持的颜色丰富，支持图片透明，不支持动图。
- `gif`,支持的颜色少，支持简单透明，支持动图。
- `webp`,谷歌推出的一种专门用于网页的图片格式，具备图片的所有优点，支持的颜色丰富，支持图片透明，支持动图，文件小等。
- `base64`，将图片转为base64编码以字符串形式存储，一般用于小图片。

## 内联框架的使用

```html
<iframe scr="https://baidu.com" />
```

## 音频标签的注意事项（视频标签类似）

### 常用属性

- controls，显示控制面板。
- autoplay，自动播放（chrome不起作用）。
- loop，循环播放。
- muted，静音。

### 使用方式

```html
<!-- 只有一个播放源 -->
<audio src="https://audio.com/test.mp3" controls />

<!-- 有多个播放源，同样可以用在视频和图片标签中 -->
<audio controls>
  <source src="https://audio.com/test.mp3" type="audio/mpeg" />
  <source src="https://audio.com/test2.mp3" type="audio/mpeg" />
  <source src="https://audio.com/test3.mp3" type="audio/mpeg" />
</audio>
```

### 不支持时的后退

在不支持音频标签时，显示音频标签内的文本内容。

## 表格标签的注意事项

### 标签分类

- `table`
- `thead`
- `tbody`
- `tfoot`
- `tr`，表示表格行。
- `th`，表示表头的单元格。
- `td`，表示单元格。
