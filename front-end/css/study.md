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

### font-weight属性值的注意事项

可以用正整数表示粗细，也可以用字面量表示。

- `normal`，400。
- `bold`，700。

## text-align的文字对齐方式

由于单词长度过长，不能在一行放下而出现换行，导致每行文字没有填满而产生空白区域。

- `left`，左对齐。
- `right`，右对齐。
- `justify`，两端对齐。
- `center`，中间对齐。

## vertical-align的注意事项

控制内联元素和表格单元格内容的垂直对齐方式。

- `top`，顶端对齐。
- `middle`，中端对齐。
- `baseline`，基线对齐。
- `bottom`，底部对齐。
- 整数，相对基线的对齐（对齐基线为0），上为正，下为负。
- 百分数，同整数一样相对基线对齐，百分数参照行高。

## text-decoration的注意事项

### text-decoration的作用

可以设置不同位置的多条线的统一样式，如位置、颜色、样式

### text-decoration-line的分类

1. `overline`，顶部的线。
2. `line-through`，中间的线。
3. `underline`，底部的线。

### text-decoration-color的作用

指定线的颜色。

### text-decoration-style的分类

1. `wavy`，波浪线。
2. `solid`，实线。
3. `daashed`，虚线。

### text-decoration-thickness的作用

设置线的粗细。

## white-space、word-break、overflow-wrap（word-wrap）的区别

- white-space，控制空白字符的显示，同时还能控制是否自动换行。它有五个值：normal | nowrap | pre | pre-wrap | pre-line。
- word-break，控制单词如何被拆分换行。它有三个值：normal | break-all | keep-all。
- word-wrap（overflow-wrap）控制长度超过一行的单词是否被拆分换行，是word-break的补充，它有两个值：normal | break-word。

## initital、inherit、unset、revert、all的区别

- `initial`，设置为CSS属性的默认值。
- `inherit`，继承父元素的同名属性的值。
- `unset`，属性可继承则同`inherit`，不可继承则同`initial`。
- `revert`，恢复成浏览器默认设置的样式。
- `all`，是一个属性，值有`initial`、`inherit`、`unset`和`revert`，可以将选择器中的所以属性统一设置值。

## background的设置

### background-repeat的作用

- `repeat`，图片在水平和垂直方向都重复。
- `repeat-x`，图片只在水平方向重复。
- `repeat-y`，图片只在垂直方向重复。

### background-attachment的作用

- `local`，滚动时，图片粘在文字上。
- `scroll`，滚动时，图片粘在元素上。
- `fixed`，滚动时，图片粘在视口上。

### background-origin的作用

除了没有`text`属性，其他的同`background-clip`。

### background-clip的作用

- `border-box`，图片裁剪到border。
- `padding-box`，图片裁剪到padding。
- `content-box`，图片裁剪到content。
- `text`，图片裁剪到文字，要显示出来要设置`color: transparent`。

### background-position的作用

- 只有一个参数，设置对应方向，另一个方向为`center`。
- 两个参数，设置对应两个方向的值。

### background-size的作用

- 只有一个参数。
  - 为数值，设置宽，高为`auto`。
  - 为`cover`，将图片铺满。
  - 为`contain`，将图片完整显示。
- 两个参数分别设置宽和高。

### background的写法

`background: background-color background-image background-repeat background-position/background-size background-origin background-clip background-attachment`。

- `background-postion/background-size`，用`/`隔开。
- `background-origin`必须写在`background-clip`前面。

## 线性渐变的注意事项

### 使用范围

只能在图片上设置，也即只能在`background`或`background-image`上设置。

### 书写方式

`background[-image]: linear-gradient([方向，]多个颜色简便值)`。

### 方向表示方法

1. 不写，默认从上至下。
2. `to`加上单个或组合`top`、`left`、`right`、`bottom`。
3. `度数deg`，顺时针转动，表示渐变方向的终点，如`0deg`表示从下至上渐变。
4. `数字turn`，顺时针转动，表示转动的圈数。

## 径向渐变的注意事项

### 使用范围

只能在图片上设置，也即只能在`background`或`background-image`上设置。

### 书写方式

`background[-image]: radial-gradient([径向渐变大小][at 方向，]多个颜色简便值)`。

## 表格样式的注意事项

- `border-space`，用于调整表格边框和单元格边框之间的距离。`border-collapse: collapse`会让`border-space`失效。
- `border-collapse`，用于合并表格边框和单元格边框,使用单元格边框的样式，去掉表格边框的样式。
- `table-layout`，有`auto`和`fixed`两个值。表格布局有两种算法，第一种列的宽度由列的最大的单元格动态决定。第二种列的宽度由列的第一个单元格宽度决定。第二种算法可以加速渲染。

## 过渡的注意事项

### 过渡的设置

- `transition-property`，过渡的属性，必须是可以变化的数值，比如属性值为`margin：0 auto`变化到`margin: 0 70px`就不可以使用过渡，因为`auto`不是可变化的值。不指定属性名，可以使用`all`。
- `transiition-duration`，过渡的时间，
- `transition-timing-function`，过渡的速度变化，可以使用`cubic-bezier`曲线函数。
- `transition-delay`，过渡的延迟时间。
- `transition`，过渡的总写方式，不管是总写还是分开写，需要写多个过渡属性的，用逗号隔开。

### 可以使用过渡的属性

必须是个可以变化的值，否则不生效。

### transition-timing-function常用的属性值

- `linear`,匀速。
- `ease`，慢速开始和慢速结束。
- `ease-in`，慢速开始。
- `ease-out`，慢速结束。
- `ease-in-out`，同`ease`类似。
- `cubic-bezier(x,y,x2,y2)`函数。
- `steps`，第一个参数为分几步完成，第二个参数为是每步的开始还是结束显示，默认为结束。

## 动画的注意事项

### 动画的设置

- `animation-name`，动画的名称。
- `animation-duration`，动画时间。
- `animation-timing-function`，动画的速度变化，类似过渡。
- `animation-delay`，动画的延迟。
- `animation-iteration-time`，动画次数，`infinate`表示无限循环。
- `animation-direction`，动画方向，`normal`默认值，从`to`到`from`，`reverse`从`from`到`to`。`alteranate`从`to`到`from`，从`from`到`to`循环。`alternative-reverse`从`from`到`to`，从`to`到`from`循环。
- `animation-fill-mode`，`none`为默认，`backwards`表示在等待动画的时候用第一帧的样式，`forwards`动画结束后，用最后一帧的样式，`both`表示`backwards`和`forwards`同时生效。[详细看这里](https://www.cnblogs.com/lyzg/p/5738860.html)
- `animation-play-state`，控制动画的运动状态，`paused`表示动画暂停，`running`表示动画启动。

### 动画的书写形式

1. 动画的声明

```css
@keyframes animate {
  0% /* 也可以写成from */ {}
  25% {}
  /* ... */
  100% /* 也可以写成to */ {}
}

.animate {
  /* animation: 动画名称 持续时间 延迟时间 时间函数 动画次数 动画方向 动画状态 */;
}
```

## transform的注意事项

### 百分比单位的使用

相对于自身，`left`、`top`这些是相对于定位父元素。

### 坐标系的使用

- x轴从左往右，为负数到正数。
- y轴从上至下，为负数到正数。
- z轴从内向外，为负数到正数。

### transform的类型

- translate，平移。
- rotate，旋转。
- scale,伸缩。
- skew，歪斜。

### transform-origin的使用

调整变换原点的位置。

## 多个变换的注意事项

当书写多个变换时，用空格隔开，且变换有顺序，为书写的顺序。

## backface-visibility的使用

当页面具有3的效果时，对元素进行翻转，并看不到元素后面的内容，可以通过设置`backface-visibility: visible`来达到这个效果。

## perspective的使用

为了让元素z轴放大缩小，有近大远小的效果，可以使用`perspective`调整观察者的视角距离。

## perspective-origin的使用

调整观察者的位置。

## CSS变量的使用

- 设置变量，`--变量名`。
- 使用变量，`var(变量名)`。

## CSS计算函数的使用

使用`calc(表达式)`可以计算数据返回计算后的值。

## 弹性盒模型布局的使用

### 哪些元素可以使用弹性盒模型？

块状元素（`display: flex`）和内联元素（`display: inline-flex`）都可以。

### 使用注意事项

- 父元素定位弹性盒子后，子元素的`float`、`clear`和`vertical-align`将失效。
- 被定义为弹性盒的父元素被称为`Flex的容器`，子元素被称为`Flex的项目`。
- `Flex盒子`内有两个轴，一个是水平的主轴，另一个是垂直的交叉轴。

### 常用的属性

#### 属性分类

1. 只用于容器上的属性。

  1. `flex-direction`，定义主轴的方向。
  2. `flex-wrap`，默认情况，所有项目都仅在一个行上，该属性定义项目一行放不下时，如何换行。
  3. `flex-flow`，组合了`flex-direction`和`flex-wrap`。
  4. `justify-content`，定义了主轴上项目的排列方式。
  5. `align-items`，定义了项目在交叉轴上的的排列方式。
  6. `align-content`，定义了多根轴线（多个项目占据多行时，交叉轴上）的排列方式，如果只有一条轴线不起效果。

2. 只用于项目上的属性。
   1. `order`，定义项目的排列顺序，为整数，从左至右，从小至大（默认值为0）。
   2. `flex-grow`，定义了项目总长小于主轴长度时，项目在主轴上的放大比例（默认值为0,即不放大）。
   3. `flex-shrink`，定义了当项目总长大于主轴长度时，项目在主轴上的缩小比例（默认值为1,即等比例缩小），
   4. `flex-basis`，定义了在分配剩余空间之前，项目占据主轴长度的多少（默认值为auto，即项目本来的大小）。
   5. `flex`，组合了`flex-grow`、`flex-shrink`和`flex-basis`，书写形式为`flex: <flex-grow> <flex-shrink> || <flex-basis>`，默认值为`flex: 0 1 auto`;有两个特殊属性`none`和`auto`，`none`为`0 0 auto`，`auto`为`1 1 auto`。
   6. `align-self`，定义了项目在交叉轴上的对齐方式，默认值为`auto`，即继承容器中`align-items`定义的属性值。其他属性同`align-items`。

#### flex-direction的属性值

1. `row`，从左至右（默认值）。
2. `row-reverse`，从右至左。
3. `column`，从上至下。
4. `column-reverse`，从下至上。

#### flex-wrap的属性值

1. `nowrap`，不换行（默认值）。
2. `wrap`，在下面起新行。
3. `wrap-reverse`，在上面起新行。

#### flex-flow的书写方式

`flex-flow: <flex-direction> || <flex-wrap>`，默认值为`flex-flow: row nowrap`;

#### justify-content的属性值（align-content类似）

1. `flex-start`，主轴的开始（默认值）。
2. `center`，主轴的中间。
3. `flex-end`，主轴的末尾。
4. `space-between`，两端对齐。
5. `space-around`，每个项目的两侧空白等距。
6. `space-evenly`，`evenly`为平均的含义，不同于`space-around`，`space-evenly`让项目之间的空白等距。

#### align-items的属性值

1. `flex-start`，交叉轴的开始。
2. `center`，交叉轴的中间。
3. `baseline`，根据文字的基线对齐。
4. `flex-end`，交叉轴的末尾。
5. `stretch`，沿交叉轴上下拉伸铺满（默认值）。


## 网格布局的使用

### 弹性盒模型布局和网格布局的区别

网格布局可看成一维布局，利用主轴进行布局，网格布局可看成二维布局，利用行和列产生的单元格进行布局。

### 哪些元素可以使用弹性盒模型？

块状元素（`display: grid`）和内联元素（`display: inline-grid`）都可以。

### 网格的形成

由行和列交叉构成网格，`n`行和`m`列可以组成`n * m`个单元格的表格，等价于`n+1`个行线和`m+1`个列线组成。

### 使用注意事项

- 网格布局的父元素叫容器，子元素叫项目。
- 同弹性盒模型布局，网格布局的属性分为容器属性和项目属性。

### 容器属性

1. `display: grid || inline-grid`，定义当前元素为网格布局的容器。
2. `grid-template-columns`，定义列宽。
3. `grid-template-rows`，定义行高。
4. `grid-auto-columns`和`grid-auto-rows`同上，也是指定列宽和行高的，但是作用于当指定单元格不在生成的单元格中时，自动生成的单元格列宽和行高，不指明的情况下，自动生成的网格的列宽和行高为前两条指定的。
5. `grid-template-areas`，定义单元格区域名称，指定单元格后，网格线会自动命名，如`grid-template-areas: header header header`,则起始网格线名`header-start`，末尾网格线名`header-end`。
6. `grid-auto-flow`，定义了网格布局中项目的填充方式，默认值为`row`，从左至右，从上至下填充项目，`column`，从上至下，从左至右，`row dense`和`column dense`，定义了当项目不够排列一行时，换行导致上一行留下的空白的填充方式，`column`和`row`会不进行填充，按顺序排列，而加上`dense`后，会让后面够小的项目填充到前面。
7. `row-gap`，定义行之间的间距。
8. `column-gap`，定义列之间的间距。
9. `gap`，组合`row-gap`和`column-gap`，格式`gap: <row-gap> <column-gap>`，如果只写一个值则默认为行间距和列间距的值。
10. `justify-items`定义了单元格项目中内容的水平排列方式（列的排列方式），`align-items`定义了单元格项目中内容的垂直排列方式（行的排列方式），`place-items`组合了`align-items`和`justify-items`，书写方式`place-items: <align-items> || <justify-items>`，当只有一个值时，表示为`align-items`和`justify-items`的值。属性值有`start`、`center`、`end`、`stretch`。
11. `justify-content`、`align-items`和`place-content`类似上一条，但是表示的是所有单元个在容器中的排列，多了几个属性：`space-between`、`space-around`、`space-evenly`。
12. `grid-template`组合了`grid-template-columns`、`grid-template-rows`和`grid-template-areas`，但是不容易书写。，不推荐。
13. `grid`同上，组合了所有的属性，不利于书写，不推荐。

### 项目属性

- `grid-row-start`，指定单元格的水平起始线位置或名称，可以使用`span 单元格位置`，表示跨一个格子。
- `grid-row-end`，指定单元格的水平终止线位置或名称，可以使用`span 单元格位置`，同`grid-row-start: span 单元格位置`效果一样。
- `grid-row`，指定单元格的水平起始线和终止线的位置，格式`grid-row: <grid-row-start>[ / <grid-row-end>]`。可以省略斜杠后的值，默认跨一个单元格，同样可以给`<grid-row-end>`写为`span 单元格位置`表示跨几个单元格。
- `grid-column-start`，指定单元格的垂直起始线位置或名称，可以使用`span 单元格位置`，表示跨一个格子。
- `grid-column-end`，指定单元格的垂直终止线位置或名称，可以使用`span 单元格位置`，同`grid-column-start: span 单元格位置`效果一样。
- `grid-column`，指定单元格的垂直起始线和终止线的位置，格式`grid-column: <grid-column-start>[ / <grid-column-end>]`。可以省略斜杠后的值，默认跨一个单元格，同样可以给`<grid-column-end>`写为`span 单元格位置`表示跨几个单元格。
- `grid-area`，用于指定当前的项目位于容器下哪个区域，可以使用区域名指定或位置名称指定。格式`grid-area: <区域名称> || grid-row-start> / <grid-column-start> / <grid-row-end> / <grid-column-end>;`
- `justify-self`、`align-self`和`place-self`用于设置项目内容的排列方式，不设置则继承`justify-items`、`align-items`和`place-items`的样式设置。

### repeat函数的使用

在定义很多网格时，可以使用`repeat`函数避免重复书写，格式`repeat(重复次数，值 || 多个值)`。重复的次数可以使用`auto-fill`来自动填充。

### fr的使用

`fr`也即`fraction 片段`，例如`grid-template-columns: repeat(10, 1fr 2fr)`，表示后一个列宽是前一个列宽的两倍，重复十次。

### minmax函数的使用

定义列宽或行高的区间，格式`minmax(100px, 1fr)`，表示最小值100px，最大值1fr。

### auto关键字

表示浏览器来决定列宽和行高的大小，如`grid-template-columns: 100px auto 100px`，表示左右列宽100px,中间的宽度自适应。

### 指定网格线名称的方式

- 可以在`grid-template-columns || grid-template-rows`中在设置列宽或行高的同时，通过`[网格线名称[ 网格线名称2 网格线名称3 ...]]`的方式，设置网格线的名称，方便以后使用

  1. `grid-template-columns: [title-start] 100px [title-end content-start] 200px [content-end] `
  2. `grid-template-rows: [title-start] 100px [title-end content-start] 200px [content-end] `

- 通过`grid-template-areas`指定单元格区域名时，自动命名。

## CSS像素和视口的相关问题

CSS的像素是一个相对值，在不同的设备上有不同的`devicePixelRatio`，而视口被定位为三种：布局视口、视觉视口和理想视口。

[详细见此](https://github.com/jawil/blog/issues/21)

## vw和vh的理解

vw和vh是相对于视觉视口来定义的，`100vw`等于视觉视口的宽度，`100vh`等于视觉视口的高度。

## 网页的字体大小问题

网页中最小的网页字体为`12px`。

## 媒体查询的使用

[详细见此](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Media_Queries/Using_media_queries)