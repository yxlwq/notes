# CSS3的学习笔记

## CSS的定义理解

CSS（Cascading Style Sheet，层叠样式表），层叠的含义是指网页中的每个元素可以有多个样式来源，按照样式的优先级对样式进行叠加后得到最后的样式表。

## CSS中样式叠加的理解

在CSS中由于同一个元素的样式有多个来源，因此需要理解样式如何进行叠加。

1. 从祖先元素继承。
2. 从同一个元素同级的不同来源获得，按一下情况区分：
  
  1. CSS不同名的属性直接获得。
  2. CSS同名属性，按一下优先级区分：
  
    1. 优先级相同，后面覆盖前面。
    2. 优先级不同，优先级高的覆盖优先级低的。


## CSS的选择器分类

优先级从高到低排列。

- id选择器

`#id选择器名称`

- 类选择器

`.类选择器名称`

- 伪类选择器

`:伪类选择器名称`

- 属性选择器

```html
<style>
/* 存在name属性的元素 */
[name] {}

/* 存在name属性且属性值匹配value的元素 */
[name = value] {}

/* 存在name属性且属性值包含value的元素 */
[name *= value] {}

/* 存在name属性且属性值以value结尾的元素 */
[name $= value] {}

/* 存在name属性且属性值以value开头的元素 */
[name ^= value] {}

/* 存在name属性且属性值包含以空格分隔value的元素 */
[name ~= value] {}

/* 存在name属性且属性值以value开头的元素 */
[name |= value] {}
</style>
```

- 元素选择器

`元素名 {}`

- 伪元素选择器

`::伪元素名 {}`

- 通用选择器

`*`

- 分组选择器

`选择器1, 选择器2`

- 后代组合器

`祖先选择器1 后代选择器2`


- 直接子代组合器

`父选择器1 > 子选择器2`


- 一般兄弟组合器

`兄弟选择器1 ~ 兄弟选择器2`

- 紧邻兄弟组合器

`兄弟选择器1 + 兄弟选择器2`


## CSS的优先级

1. !important
2. 内联样式
3. id选择器
4. 类选择器、伪类选择器、属性选择器
5. 元素选择器、伪元素选择器
6. 剩下的选择器不算优先级

## CSS的书写位置

1. 内联样式

`<div style="color: red;">块</div>`

2. 行内样式

```html
<style>
  div {
    color: red;
  }
</style>
```

3. 外部样式
  1. 用link标签引入。
  2. 在样式表中用`@import url(css位置.css)`引入。

## 不同的引入外部样式文件的方式的差异

- link属于标签，而`@import url()`属于CSS语法，且`@import url()`必须写在样式表的开头，否则无法引入。
- `@import url()`在浏览器中兼容性不同。
- link引入的文件在HTML文件加载时被同时加载，而`@import url()`引入的文件会在页面全部下载完毕后再被加载。

## CSS的注释

`/* 可以换行书写 */`。

## 常见的伪类选择器

- `:first-child`
- `:last-child`
- `:nth-child`
- `first-of-type`
- `last-of-type`
- `nth-of-type`
- `:link`
- `:hover`
- `:active`
- `:visited`

## 常见的伪元素选择器

- `::before`
- `::after`
- `::first-letter`
- `::first-line`
- `::selection`

## em和rem的区别

`em`和`rem`都是相对`font-size`设置的大小，`1em`或`1rem`等于1个`font-size`大小。元素的`font-size`的`em`是相对于父元素的`font-size`的大小，元素其他属性的`em`是相对于子元素的`font-size`的大小。

## 使用颜色的注意事项

## 颜色设置方式的区别

- rgb
- rgba
- hsl
- hsla

## rgb的含义

rgb（Red Green Blue，红绿蓝），使用红色、绿色和蓝色进行调整，单位可以是百分号`0%-100%`、每个颜色用一个字节表示`0-255`、用十六进制表示每个颜色用两个16进制位（也即一个字节）表示：`#aabbcc`，同颜色两个16进制位相同可以省略一个即`#abc`。

## rgba的含义

在rgb设置颜色的基础上，加了一个不透明度为`0%-100%`，`0%`表示完全透明，`100%`表示完全不透明。

## hsl的含义

hsl（Hue Saturation Lightness，色相 饱和度 亮度）。色相为颜色的取值，范围为`0-360`，相当于一个360度的调色盘。饱和度为颜色的浓度，范围为`0%-100%`。亮度为颜色的亮度，范围为`0%-100%`。

## hsla的含义

在hsl设置颜色的基础上，加了一个不透明度为`0%-100%`，`0%`表示完全透明，`100%`表示完全不透明。

## CSS的百分比都相对于谁？

基本都是相对于`父`级元素（实际上是`包含块`）的宽高，但是`父`不一定是真正的父级元素，如果在有绝对定位的情况下，是相对于定位上的父级元素的宽高，固定定位的元素的父级在父级没有设置`transform`为除`none`以外的属性时，父级为视口，在父级设置`transform`为除`none`以外其他属性值时，父级为位置上的父级，注意将`transform`设置在除父级以外的祖先元素上没有效果，依然是相对于视口。

[详细见此](https://www.zhihu.com/question/36079531)

## 盒模型的注意事项

### 盒模型的组成

盒模型的组成：`content + padding + border + margin`。`width/height`的设置会因为盒模型不同而改变，默认`width/height`为`content`，`IE盒模型/怪异盒模型下`的`width/height`为`content + padding + border`。

### 盒模型的分类

1. `w3c的标准盒模型`，`width/height`为`content`，盒子大小为`width/height + padding + border + margin`，`box-sizing`中的属性值为`content-box`。
2. `IE盒模型/怪异盒模型`，`width/height`为`content + padding + border`，盒子大小为`width/height + margin`。

## 值的设置

在CSS中设置属性的值有4种方式：

1. 四个值设置上、右、下、左的值。
2. 三个值设置上、左右、下的值。
3. 两个值设置上下、左右的值。
4. 一个值设置上、右、下、左的值。

## color的注意事项

color用于设置前景色和背景色，前景色包括字体颜色和边框颜色，也就是在没有设置边框颜色的情况下，`color`的设置的颜色会作用于边框上。

## 上下外边距重叠的注意事项

### 重叠的三种情况和防止方法

1. 相邻元素的上下外边距重叠，防止方法：其中一个设置BFC。
2. 父子元素，子元素有上下外边距且父元素上下没有`content`、`padding`、`border`将子元素的上下边距隔离开，子元素的上下外边距会和父元素的上下外边距重叠。防止方法：

  1. 父元素设置BFC
  2. 父元素设置`content`、`padding`、`border`其中一个。

3. 空的块状元素在没有设置`content`、`padding`和`border`时，也即上下margin挨着时，上下margin会发生重叠。防止方法：空的块状元素设置`content`、`padding`、`border`其中一个。

注：三种情况可以同时出现，情况会更复杂。

[详细看这里](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)

### 重叠值的计算

1. 都是正值，取最大。
2. 都是负值，取最小。
3. 有正有负，取`最大的正值 - 最小的负值（绝对值最大的负值）`。

## 块级子元素的在父元素中的水平布局问题

块级子元素在父元素的水平布局必须满足子元素的`水平的margin + 水平的border + 水平的padding + 水平的content`等于父元素的`content`的水平宽度，从而让块级子元素永远独占一行。

1. 如果不等于，则优先调整`content`满足上式。
2. 如果不等于，且`content`以被设置，水平的`margin`设置为`auto`时，则优先调整水平的`margin`，否则优先调整`margin-right`。

## 浮动后的元素宽度不会虽父元素宽度变化的问题

块级元素由于有水平布局的机制，因此不用设置宽度，会优先随着父盒子宽度变化。但是浮动后的元素不再是块状元素了，而是内联块状元素，没有了块状元素计算水平宽度的机制，因此需要手动设置宽度。

## 块级格式化上下文的注意事项

### 块级格式化上下文是什么？

块级格式化上下文又称BFC（Block Formatting Context），BFC是一个特殊的区域，与外界区域相互隔绝，无法相互影响。

[详细了解BFC](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

### 常见的产生BFC的条件

- html标签
- `display: flow-root`，这个设置方法没有副作用。
- 浮动
- 定位中的`absolute`和`fixed`
- `overflow`除默认值`visible`的其他值。
- 弹性元素
- 网格元素
- 内联块状元素`inline-block`
- 表格单元格和标题

### BFC的使用场景

- 包含内部浮动（父子元素，子元素浮动且有高度，父元素没设置高度，此时父子元素不等高）
- 排除外部浮动（前一个元素浮动，后一个元素占据浮动元素的位置）
- 阻止外边距重叠

### Reset.css和Normalize.css的演变

`Reset.css`和`Normalize.css`都是为了解决不同浏览器默认样式造成的影响。`Reset.css`暴力去除默认样式，而`Normalize.css`则追求不同浏览器默认样式的统一化，而不是暴力去除不好的默认样式。

## line-height的注意事项

### line-box的理解

行盒子是一个看不见但是真实存在的盒子，`line-height`设置的就是行盒子高度，行
盒子用于存放文字，盒子是从文字的中间向上下展开。我理解的行盒子是在`margin、border、padding、content`中的`content`中，如果`height`没有设置，行高可以撑开`height`，如果设置`height`，行盒子高度如果超出`content`的`height`，可以使用`overflow: hidden`进行隐藏。每行文字都会有一个行盒子,因此一个`content`可以有多个行盒子。

## line-height的使用场景

- 单行文字居中。在块级元素中的单行文字，可以利用`line-height`等于块级元素的`content`的高度，实现居中。
- 多行文字可以利用`line-height`设置每行文字中线之间的距离。

## outline的注意事项

`outline`位于`border`的外层，设置方法和`border`一致，但是不占据位置，只有显示效果。

## box-shadow的注意事项

- 盒子的阴影大小同盒子一致，为`border + padding + content`，位于盒子的内部，被盒子遮住，但是同`outline`不占据空间，且都是从`border`的外层延伸而出。
- 设置方式`box-shadow: 10px 10px 10px red`。第一个为横向偏移量，第二个为垂直偏移量，第三个参数为模糊半径，第四个参数为扩散半径（将盒子沿着中心点延伸），第五个参数为阴影颜色。
- 需要多个阴影时，用逗号隔开。

## border-radius的注意事项

### border-radius设置什么？

`border-radius`用于设置盒子四个角上的圆的半径，每个圆都与两个相邻边相切，并将圆和对应的角之间的多余区域切除。

### border-radius设置值的方式

- 一个值，设置四个角上圆的半径。
- 两个值，分别表示左上/右下、右上/左下的角上圆的半径。
- 三个值，分别表示左上、右上/左下、右下的角上圆的半径。
- 四个值，分别表示左上、右上、右下、左下的角上圆的半径。

### 单独设置每个角的方式

1. 左上：`border-top-left-radius`。
2. 右上：`border-top-right-radius`。
3. 右下：`border-bottom-right-radius`。
4. 左下：`border-bottom-left-radius`。

### border-radius常见的使用场景

- 将盒子切割成圆，设置`border-radius：50%`。
- 将盒子切割成胶囊，设置`border-radius：1em`。

## float的注意事项

### float的特点

- 脱离正常流，不再占据正常流的位置。
- 不会脱离父元素的范围。
- 不会超过前面的位置，也即当前面是不浮动元素，则不会向前移动，若是浮动元素则和前面的浮动元素并排一行
- 可以向左或向右浮动。

### clear的使用

`clear`可以用于清楚浮动元素对当前的影响。有三个属性值：

1. `left`，清除左浮动元素对当前元素的影响。
2. `right`，清除右浮动元素对当前元素的影响。
3. `both`，清除左浮动和右浮动元素对当前元素的影响。

### 如何解决浮动的子元素导致父盒子高度坍塌问题？

1. 给父盒子生成BFC。
2. 利用清除浮动的方式，可以给父元素的内部末尾加上伪元素`::after`，且给其设置成块状元素。

## 元素的定位注意事项

### 元素的定位方式

1. static，静态定位，默认值。
2. relative,相对定位，相对与自己原有位置定位，依然占据正常流的位置，没有变为内联块状元素。
3. absolute，绝对定位，相对于有除静态定位的其他定位的祖先元素定位，脱离文档流，变成内联块状元素。
4. fixed，固定定位，类似绝对定位的特性，只是当父元素（只在父元素上设置有效果）设置了除`none`属性值的其他`transform`设置时，相对于父元素定位，其他都相对于视口定位。
5. sticky，粘性定位，相对于最近的可以滚动的祖先定位，同相对定位不会脱离正常流，还占据原有位置。`top`属性设置距离祖先元素顶部距离多少时粘住，当同时设置多个同级元素为粘性定位时，下一个粘性定位元素会顶掉上一个粘性定位占据的位置。最近的不可滚动的祖先设置`overflow`为`hidden`、`auto`、`scroll`这些属性，会导致需要被粘住的滚动祖先失效。

### z-index、top、right、bottom和left的适用对象

- z-index的适用对象：

  1. relative
  2. abosulte
  3. fixed

- top、right、bottom和left的适用对象为除`static`以外的定位。

### z-index的使用

只能用整数，默认值为0，从负数到正数，向观察者靠近。

## font的使用注意事项

### 参数类型分类

- `font-size`，字体大小，必写。
- `font-family`，字体家族，必写。
- `font-weight`，字体粗细。
- `font-style`，字体样式。
- `line-height`，行高，可以和`font-size`一起写，格式为`font-size/line-height`。
- `font-variant`，字体变体。

### 引入自定义字体的方式

```css
@font-face {
  font-family: '自定义名称';
  src: url('引入字体文件的位置'); /* url可以引入多个，用逗号隔开，作用是防止字体文件的导入出问题。 */
}
```

### 字体图标的优点

- 体积小
- 加载快
- 灵活性高，可向字体一样修改样式
- 可直接改变颜色。


