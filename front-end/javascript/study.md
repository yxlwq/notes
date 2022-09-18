# JavaScript学习笔记

## 计算机语言的分类

机器语言、汇编语言和高级语言。计算机只认识机器语言，高级语言需要被解析成机器语言后，计算机才能认识它。

## ECMAScript标准

由ECMA（European Computer Manufactures Association，欧洲计算机制造商协会）下的TC-39（Technical Committee 39，39号技术委员会）负责编写，编号为ECMA-262。

## JavaScript的组成

1. ECMAScript
2. BOM（Browser Oject Model，浏览器对象模型）
3. DOM（Document Object Model,文档对象模型）

## 语言的解析方式

### 分类

1. 解释型语言（JavaScript）
2. 编译型语言

### 区别

解释型语言会对代码从上至下，从左至右逐行解析和执行。编译型语言对代码的整体进行编译，生成可执行的编译文件。

## JavaScript的编写位置

1. 嵌入

```html
// my.html
<script type="text/javascript">
// js代码内容
</script>
```

2. 外部引入（推荐）

```html
// my.html
<script type="text/javascript" src="my.js"></script>
```

3. 标签属性

```html
// my.html
<button onclick="alert('激活')">click</button>
<a href="javascript:alert('激活');">普通按钮</a>
<a href="javascript:;">普通按钮</a>
```

## JavaScript中常见的名词

- 字面量
- 常量
- 标识符
- 关键字
- 保留字

## JavaScript的数据类型

### 分类

1. 基本数据类型
   1. String
   2. Number
   3. Boolean
   4. Null
   5. Undefined
2. 引用数据类型
   1. Object

### String

#### 类型转换

- toString

除了Null和Undefined数据类型没有toString方法，其他数据类型都可以使用`data.toString()`获得该数据类型的字符串形式。

```javascript
var data;

// Number
data = 1;
console.log(data.toString()); // '1'

// Boolean
data = true;
console.log(data.toString()); // 'true'

// Array
data = [1,2,3];
console.log(data.toString()); // '1,2,3'
data = [];
console.log(data.toString()); // ''

// Object
data = {};
console.log(data.toString()); // '[object Object]'
data = {a: 1};
console.log(data.toString()); // '[object Object]'

// 正则表达式
data = /a/i;
console.log(data.toString()); // '/a/i'

// function
data = function () {};
console.log(data.toString()); // 'function () {}'
```

- String

输出同`toString`，但是解决了Null和Undefined不能使用`toString`的缺陷。

```javascript
console.log(String(null)); // 'null'
console.log(String(undefined)); // 'undefined'
```

#### 转义字符`\`

- `\\`，表示`\`
- `\"`，表示`"`
- `\'`，表示`'`
- `\n`，换行符
- `\t`，制表符
- `\u` + 四位十六进制编码，表示字符

### Undefined

#### 含义

`undefined`表示数据已经被声明，但是未被赋值。

###  Null

#### 含义

`null`表示数据为一个空对象。

### Number

#### 进制表示

1. 二进制
```javascript
// 十进制的8
console.log(0b1000); // 8
// 
```

2. 八进制

```javascript
// 十进制的8
console.log(010); // 8
```

3. 十进制
4. 十六进制

```javascript
// 十进制的16
console.log(0x10); // 16
```

#### 类型转换

- Number

```javascript
var data;

// String
// 纯数字
data = '123';
console.log(Number(data)); // 123
// 空字符串
data = '';
console.log(Number(data)); // 0
// 其他非数字字符串
data = '123px';
console.log(Number(data)); // NaN

// Boolean
data = true;
console.log(Number(data)); // 1;
data = false;
console.log(Number(data)); // 0;

// Array
// 空数组
data = [];
console.log(Number(data)); // 0
// 只有一个数字或字符串数字的数组
data = [200];
console.log(Number(data)); // 200
data = ['200'];
console.log(Number(data)); // 200
// 其他
data = [1,2,3];
console.log(Number(data)); // NaN

// Object
data = {};
console.log(Number(data)); // NaN
data = {a: 1};
console.log(Number(data)); // NaN

// function
data = function () {};
console.log(Number(data)); // NaN

// 正则
data = /a/i;
console.log(Number(data)); // NaN
```

- parseInt

用于将字符串转为整数。解决了Number函数无法解析八进制数，`123px`解析为`NaN`和空字符串转为`0`的问题。

注意：**Number和parseInt转换八进制的字符串数字，会将前面的0去掉，按照十进制解析，因此，parseInt提供第二个参数表明解析几进制数**

- parseFloat

用于将字符串转为浮点数。

#### 浮点数计算的问题

```javascript
// javascript中，浮点数计算不精确
console.log(0.1 + 0.2); // 0.3000...4
```

#### 字面量

- Number.MAX_VALUE
- Number.MIN_VALUE
- Number.POSITIVE_INFINITY，也即`Infinity`
- Number.NEGATIVE_INFINITY，也即`-Infinity`
- `NaN`

### 检查类型

- typeof

```javascript
var data = 1;
console.log(typeof data); // number

data = '1';
console.log(typeof data); // string

data = true;
console.log(typeof data); // boolean

data = null;
console.log(typeof data); // object


data = undefined;
console.log(typeof data); // undefined

data = function () {};
console.log(typeof data); // function

data = /a/i;
console.log(typeof data); // object

data = [];
console.log(typeof data); // object

data = {};
console.log(typeof data); // object
```

### Boolean

#### 类型转换

- Boolean

```javascript
var data;

// String
// 空字符串
data = '';
console.log(Boolean(data)); // false
// 其他字符串
data = 'false';
console.log(Boolean(data)); // true

// Number
// 0
data = 0;
console.log(Boolean(data)); // false
// NaN
data = NaN;
console.log(Boolean(data)); // false
// 其他数字
data = -1;
console.log(Boolean(data)); // true
data = -Infinity;
console.log(Boolean(data)); // true
data = Infinity;
console.log(Boolean(data)); // true

// Null
data = null;
console.log(Boolean(data)); // false

// Undefined
data = undefined;
console.log(Boolean(data)); // false

// Object，Array，正则表达式，函数，都为true
data = [];
console.log(Boolean(data)); // true
data = {};
console.log(Boolean(data)); // true
data = function () {};
console.log(Boolean(data)); // true
data = /a/i;
console.log(Boolean(data)); // true
```

### Object

#### 对象分类

1. 内建对象，JavaScript自带的对象，如：Array、Function等。
2. 宿主对象，JavaScript运行环境自带的对象，如：Date等。
3. 自定义对象

#### 查找对象属性

使用`in`和`hasOwnProperty`判断对象是否存在该属性名，`in`会查找原型链，`hasOwnProperty`不会查找原型链。

#### 创建对象的属性运用

在JavaScript中标识符必须为字符串，且只能由字母、数字、`_`和`$`组成，第一位不能为数字。但是对象的属性名用`对象[名]`的方式为对象创建属性，该属性可以为数字开头的字符串，也可以是任何数据类型，包含对象，引用是也只能通过`对象[名]`的方式引用。

```javascript
let event = {};
let time1 = new Date();
let thing1 = function () {};
event[time1] = thing1;
console.log(event[time1]);

// 或者
let event = {
   [time1]: thing1,
};
console.log(event[time1]);
```

#### 变量构建过程

基本数据类型创建在栈内存中。引用数据类型创建在堆内存中，在栈内存中存放指向该堆内存的地址。

#### 全局对象window的注意事项

全局变量，会作为`window`对象的属性保存，用`let`声明的全局变量，不会被`window`的属性保存。

```javascript
var data = 0;
console.log(window.data); // 0

let data2 = 0;
console.log(window.data2); // undefined

function func () {};
console.log(typeof window.func); // 'function'

let func2 = function () {};
console.log(typeof window.func2); // undefined
```

### 构造函数注意事项

#### 新建实例的过程

1. 新建空对象
2. 空对象的原型指向构造函数的原型
3. this指向该对象
4. 返回该对象

#### 原型链的理解

每个构造函数有一个原型，用于存放实例的共用数据，原型可以通过`构造函数.prototype`访问，原型同样可以通过`原型.constructor`来访问构造函数，原型还可以通过`原型.__proto__`访问父构造函数的原型，构造函数的实例通过`实例.__proto__`访问构造函数的原型。

![原型链的结构](./images/%E5%8E%9F%E5%9E%8B%E9%93%BE.png)

#### 属性查找

现在实例的属性上查找，再到原型链上查找，直到找到`Object.prototype`，没有则返回undefined。

#### 构造函数实例的判断

通过`实例 instanceof 构造函数`的返回值来判断该实例是否是该构造函数的实例。原理为查找该实例的原型链上能否找到构造函数的原型，找的到返回真，否则返回假。

```javascript
// 模拟instanceof执行过程

let cls = function () {}
let instance1 = new cls();

function instanceOf(l, r) {
    let chains = l.__proto__;
    let target = r.prototype;
    do {
        if (chains === target) return true;
        chains = chains.__proto__;
    } while (chains != null);
    return false;
}

console.log(instanceOf(instance1, cls)); // true
```

## String的注意事项

### 字符串的正则表达式的方法

1. search

查找指定字符串或者正则表达式指定的内容所在的位置，没有返回-1

2. match

查找指定字符串或者正则表达式指定的内容的详情，返回的是数组。

3. replace

第一个参数为字符串或正则表达式，表示要被替换的内容，第二个参数为要替换的内容。

4. split

以指定字符串或正则表达式代表的内容进行分割。

### 字符串的存储

在JavaScript中，字符串底层用数组存储字符串。

```javascript
var s = 'abc';
console.log(s.length); // 3
console.log(s[1]); // 'b'
```

### charAt、charCodeAt、String.fromCharCode的使用

charAt返回指定下标的字符，charCodeAt返回指定下标的字符的Unicode编码，String.fromCharCode返回指定Unicode编码的字符。

### indexOf、lastIndexOf的使用

都是用于返回指定字符的下标，第二个参数是开始的位置。indexOf从左向右查找，lastIndexOf是从右向左查找。

## RegExp的注意事项

### 常用语法

- `{n}`，表示匹配前面字符n次
- `{n,m}`，表示匹配前面字符n-m次
- `{n,}`，表示匹配前面字符n次以上
- `n?`，也即`{0,1}`
- `n+`，也即`{1,}`
- `n*`，也即`{0,}`
- `.`，表示任意字符
- `\w`，匹配字母数字下划线，相当于`[A-z0-9_]`
- `\W`，匹配非单词，相当于`[^A-z0-9_]`
- `\s`，匹配空白字符
- `\S`，匹配非空白字符
- `\d`，匹配数字，相当于`[0-9]`
- `\D`，匹配非数字，相当于`[^0-9]`

```javascript
// \d，单词边界的理解
let reg = /word/i;
let s = 'myWord';
s.match(reg); // 能匹配到myWord里的Word
let reg2 = /\bword\b/i;
s.match(reg2); // 不能匹配到myWord的Word，只能匹配单个word
'word'.match(reg2); // 能匹配到word
```

### 正则表达式的创建

构造函数RegExp的参数第一个是正则表达式，第二个是匹配模式。

### 匹配模式

1. `i`，忽略大小写
2. `g`，全局匹配

### `[^ ]`的使用

匹配除了括号里的其他内容。

## Math的注意事项

### ceil的使用

向上取整，小数位只要有值，直接进位。

### round的使用

四舍五入。

### floor的使用

向下取整，小数位直接去掉。

### random的使用

生成0.xxxxx的数。

```javascript
// 0-1
Math.random();

// 0-10

Math.floor(Math.random() * 10);

// 0-100

Math.floor(Math.random() * 100);
```

## Date的注意事项

### getDay的使用

获取星期几，周一到周六为1-6，周天为0。

### getMonth的使用

获取月份，0-11。

### getMiliSeconds的使用

获取当前的毫秒数，0-999。

### getTime和Date.now的使用

获取当前时间的时间戳。

## Array的注意事项

### Array构造函数实例化和字面量创建的区别

```javascript
let arr = new Array(10); // [空白*10]
let arr = [10]; // [10]
```

### length运用

- `数组.length`表示数组的最后一个数据的下一位的角标，利用这个可以末尾添加元素

```javascript
let arr = [];
for (let x = 0; x < 20; x++) {
   arr[arr.length] = x;
}
console.log(arr);
```

- `数组.length`可改变，通过改变length的值达到添加或删除数据的效果。

```javascript
let arr = [1, 2, ];
arr.length -= 1; // [1]
arr.length += 1; // [1,,]
```

### Array.prototype.sort理解

`sort`方法的参数为函数，函数有两个参数，分别是数组的前一个和后一个数据，当函数返回值大于0，前后翻转，当小于0,前后不变。

```javascript
let arr = [1,2,3,4];

// 升序
arr.sort((a, b) => a - b); // [1,2,3,4]

// 降序
arr.sort((a, b) => b - a); // [4,3,2,1]
```

## Function的注意事项

### 函数默认传入的参数

1. this
2. arguments

`arguments`是伪数组，包含了传入函数的实参，有`length`和代表函数本身的`callee`属性。

```javascript
function func() {
   console.log(func === arguments.callee);
}
func(); // true
```

### call、bind、apply的使用

都是用于改变方法的this,且执行该方法，区别call、apply立即执行，而bind返回一个函数，call和bind传入参数序列，而apply传入参数数组。

```javascript
let o = {
   a: 1,
   b: 2,
   f(x1 = 0, x2 = 0) {
      console.log(this.a + this.b + x1 + x2);
   },
};
let o2 = {
   a: 10,
   b: 20,
};

o.f.call(o2, 30, 40); // 100
o.f.apply(o2, [30, 40]); // 100
o.f.bind(o2, 30, 40)(); // 100
```

## 运算符的运用

### 算术运算的隐式转换

数据之间进行`+-*/%`时，数据本身会发生隐式转换。

1. 与字符串进行运算时，会将非字符串转换为字符串。
2. 与数字类型数据运算，非字符串会转换为数字类型。

```javascript
var data;

// 与字符串运算
data = 1 + '2';
console.log(data); // '12'

// 非字符串类型与数字运算
data = true + 1;
console.log(data); // 2
data = [] + 1;
console.log(data); // 1
data = {} + 1;
console.log(data); // '[object Object]1'
data = undefined + 1;
console.log(data); // NaN
data = null + 1;
console.log(data); // 1
```

### 一元运算符的隐式转换

使用一元运算符的数据会自动转换为数字类型。

### 自增运算符和自减运算符的注意事项

```javascript
var data = 0;

console.log(++data); // 1
data = 0;
console.log(data++); // 0
data = 0;
console.log(--data); // -1
data = 0;
console.log(data--); // 0
```

### 逻辑运算符的注意事项

#### 短路运算符的运用

```javascript
// &&，当左侧条件为真，继续执行。当左侧条件为假，短路
console.log(1 && 2); // 2
console.log(0 && 1); // 0

// ||，当左侧条件为假，继续执行。当左侧条件为真，短路
console.log(1 || 2); // 1
console.log(0 || 1); // 1
```

#### 取非的隐式转换

```javascript
// 单个取非为布尔的取反值，两个取非为布尔的值
console.log(![]); // false
console.log(!!0); // false
```

### 赋值运算符的注意事项

`+-*/%`结合`=`使用，表示对自身进行`+-*/%`运算

```javascript
var data = 0;

data += 2;
console.log(data); // 2

data = 0;
data -= 2;
console.log(data); // -2

data = 2;
data *= 2;
console.log(data); // 4

data = 3;
data /= 3;
console.log(data); // 1

data = 4;
data %= 2;
console.log(data); // 0
```

### 关系运算符的注意事项

#### 比较的方式
- 非数字比较，会先转换为数字在进行对比。
- 两个字符串比较，不会转换为数字，而是比较两个字符串的Unicode编码。

```javascript
// 两个字符串比较，按位对比，一旦有结果，立即结束比较

console.log('ac' < 'b'); // true
console.log('ca' < 'b'); // false
```

#### `==`和`===`的区别

`==`会进行隐式转换后在比较，而`===`会直接进行比较，不会隐式转换。其他运算符都会发生隐式转换，包括`>`、`>=`、`<`、`<=`。

```javascript
console.log([] == true); // true
console.log([] == true); // false

// null和undefined的==运算为true
console.log(null == undefined); // true

// NaN与任何运算都为false
console.log(true == NaN, false == NaN); // false，false
// NaN与NaN做相等运算，返回false，通过isNaN来对NaN进行比较
console.log(isNaN(NaN)); // true
```

## alert、prompt和confirm

alert返回值为undefined,prompt返回值为用户输入的值，confirm返回布尔值。

## 语句

### switch和if使用哪个

当多次比较同一个变量时，使用switch,否则使用if

### switch使用注意事项

- 每一个case必须有一个break手动断开，否则若满足一个case，会不判断条件，接着执行下一个case直至遇到break或者执行完毕。
- default为没有case满足的情况下执行。

### while和do...while的区别

while先判断条件，条件为真在执行循环体，而do...while会先执行循环体一次，之后和while一致。

### for的使用注意事项

- 第一个参数用于数据的初始化，整个for循环只执行一次，for循环前执行。
- 第二个参数用于执行循环体的判断条件，为真执行。
- 第三个参数在执行完循环体后执行。

## 利用console来计时

```javascript
console.time('timerName'); // 调用console.time设置计时器名字
setTimeout(() => console.timeEnd('timerName'), 3000); // 调用console.timeEnd结束计时，3000.xxxx
```

## 变量和函数声明的提升

在JavaScript中，使用`var`声明变量和函数的创建会在代码执行之前执行。

```javascript
console.log(data); // undefined，不会报错
var data = 1;

console.log(typeof func); // 'function' 
function func () {};

console.log(func2); // undefined，推荐使用变量声明来创建函数
var func2 = function () {};

//同名的变量和函数，函数的优先级高
console.log(typeof data2); // 'function'
var data2 = 1;
function data2 () {};
```

## this指向问题

- 普通方法中this的特点
  1. 方法执行时，this才确定。
  2. 可以改变this的指向（通过bind等方法）。
- 箭头函数中this的特点
  1. 自身没有this,向上层不断查找。
  2. 不可以改变this的指向，在箭头函数被定义时，就已经确定。

## JavaScript中的内存管理方式

1. 引用计数，无法解决循环引用
2. 标记-清除（推荐）

## 包装类的注意事项

1. Number
2. String
3. Boolean

使用上面的构造函数，可以创建对象。

```javascript
var num = 1;
console.log(num.toString()); // '1'

// 为什么可以使用方法？js中会临时将num用Number包装类包装成对象
var numObj = new Number(num);
console.log(numObj.toString());
// 使用valueOf，得到原来的值
num = numObj.valueOf();
console.log(num);

// 进一步理解
num.a = 1; // 想设置num的a属性，num被包装成对象，设置a为1，然后num又被转为值。
console.log(num.a); // num被包装类包装成Number对象，但是Number对象的原型上没有a属性，因此返回undefined

// 有包装类的存在，使得基础数据类型能够作为类的实例访问类的原型上的方法
```

## DOM的注意事项

### 节点分类

- 文档节点，代表整个网页
- 元素节点，标签
- 属性节点，标签的属性
- 文本节点，代表标签的文本内容

### 节点的属性

- nodeName
  - 文档节点为`#document`
  - 元素节点为标签名
  - 属性节点为属性名
  - 文本节点为`#text`
- nodeType
  - 文档节点为9
  - 元素节点为1
  - 属性节点为2
  - 文本节点为3
- nodeValue
  - 文档节点没有值
  - 元素节点没有值
  - 属性节点为属性值
  - 文本节点为文本内容

### 文档节点

文档节点也即doucment对象。

### onload和DOMContentloaded的区别

时机不同，onload会在网页全部渲染完成后触发，而DOMContentloaded会在dom渲染完成后触发。

### 获取节点的方法

- `document.getElementById`
- `document.getElementsByClassName`
- `document.getElementsByName`
- `document.getElementsByTagName`
- `document.querySelector`
- `document.querySelectorAll`

### 获取元素节点的子节点方法

- `节点.childNodes`
- `节点.children`
- `节点.firstChild`
- `节点.firstElementChild`
- `节点.lastChild`
- `节点.lastElementChild`

### 获取父亲节点和兄弟节点

- `节点.parentNode`
- `节点.previousSibling`
- `节点.previousElementSibling`
- `节点.nextSibling`
- `节点.nextElementSibling`

### innerHTML和innerText

- `innerHTML`用于获取HTML，`innerText`用于获取文本内容，会把内部的标签去掉，只保留文本内容。
- `innerHTML`用于设置HTML，`innerText`用于设置文本内容，如果设置HTML,也会当作文本内容输出。

### innerText和textContent的区别

innerText会遵循css样式，而textContent不会。

- 如果css中设置`display: none;`，innerText就不会输出被隐藏的文本，但是textContent会。
- innerText会和浏览器一样，将空白去掉，但是textContent会原样输出。

### outerHTML和innerHTML的区别

`outerHTML`会获取包含自身标签的所有内容，`innerHTML`会获取除开自身标签的内部的所有内容。

### innerText和outerText的区别

`outerText`和`innerText`获取文本内容没有区别，设置文本内容：`outerText`会把是自身标签也覆盖，`innerText`只会覆盖除开自身标签的内容。

### checked和selected属性

checked用于单选框和复选框，值为真选中。selected用于下拉框，值为真选中。

### document中代表元素的属性名

- `document`，文档节点
- `document.documentElement`，HTML节点
- `document.head`，head节点
- `document.body`，body节点
- `document.all`，所有节点

### document中代表类的属性

- `document.className`，类名字符串
- `document.classList`，类名的列表

### 添加和删除事件

可以使用`节点.on时间名称`设置回调，但是只能设置一个，可以使用`addEventListener`和`removeEventListener`设置和销毁多个回调函数。

- `节点.addEventListener`
- `节点.removeEventListener`
- `节点.attachEvent`，同`addEventListener`作用，用于兼容ie8，不同于`addEventListener`，其第一个参数需要加上`on事件名称`，且没有第三个参数。
- `节点.detachEvent`，同`removeEventListener`作用，用于兼容ie8，其他同上。

### 修改节点的方法

- `父节点.appendChild`
- `父节点.removeChild`
- `父节点.replaceChild`
- `父节点.insertBefore`
- `节点.setAttribute`
- `节点.removeAttribute`

### 创建节点的方法

- `document.createElement`
- `document.createAttribute`
- `document.createTextNode`

### 获取属性节点的方法

`节点.getAttribute`

### style、getComputedStyle和currentStyle的区别

- `节点.style`为行内样式，且可以修改，`window.getComputedStyle`为所有样式，不可以修改。`window.getComputedStyle`的第二个参数用于确认是否获取的是伪元素的样式，取值为'before'、'after'、null。
- `getComputedStyle`不兼容ie8，`currentStyle`兼容ie8,但不支持查看伪元素样式。

### 其他样式的相关属性

- `clientHeight`，元素的可视高度
- `clientWidth`，元素的可视高度
- `offsetHeight`，元素包含边框的可视高度
- `offsetWidth`，元素包含边框的可视宽度
- `scrollHeight`，元素的整个高度
- `scrollWidth`，元素的整个宽度
- `offsetParent`，元素的定位父元素，默认为`document.body`
- `offsetTop`，元素相对其定位父元素的顶部距离
- `offsetLeft`，元素相对其定位父元素的左侧距离
- `clientTop`，元素的顶部边框的宽度
- `clientLeft`，元素的左侧边框的宽度
- `scrollTop`，元素顶部已滚动的距离
- `scrollLeft`，元素左侧已滚动的距离

![原型链的结构](./images/DOM%E7%9A%84%E7%9B%B8%E5%85%B3%E6%A0%B7%E5%BC%8F.png)

### 事件

#### 事件对象

##### 注意事项

在ie8中，事件对象不通过函数参数形式传入，而是通过全局属性`window.event`访问。

##### 相关属性

`clientX`和`clientY`是相对于浏览器窗口左上角，而`pageX`和`pageY`是相对于整个文档的左上角，当文档出现滚轮是，两者有区别。

- `clientX`
- `clientY`
- `pageX`
- `pageY`

#### 事件的冒泡和捕获

##### 事件传播

1. 捕获阶段
2. 目标阶段
3. 冒泡阶段

从根元素向下捕获触发事件的最内层的target，并执行`addEventListener`第三个参数为`true`或者`{capture: true}`的事件处理函数，找到target后，向上冒泡，执行`addEventListener`第三个参数为`false`或者为空的事件处理函数。

##### 启用或停止事件捕获的方法

- `节点.addEventListener(事件名称，事件处理函数，true|{capture: true})`
- `节点.setCapture()`，将所有的鼠标触发的事件进行捕获到该节点上
- `节点.releaseCapture()`，取消捕获

##### target和currentTarget

由于事件有冒泡和捕获的过程，因此触发事件的不一定是最开始的那个，`target`代表触发事件最深层次的那个元素，`currentTarget`指的是当前触发事件处理函数的元素。

#### 事件委派

事件委派是利用事件的冒泡特性，提高代码执行效率的一种方式，可以给需要执行事件处理函数的元素的外层元素绑定该元素的事件处理函数，从而不需要给父元素的众多自元素一一进行事件绑定。

#### 取消冒泡的方式

- `event.stopPropagation()`
- `[window.]event.cancelBubble = true`，用于兼容ie8

#### 取消默认行为

JavaScript中在事件处理函数中返回false,可以取消默认行为，jQuery的事件处理函数中可以同时取消默认行为和停止冒泡。

- `event.preventDefault()`
- `[window.]event.returnValue = false`，用于兼容ie8

#### onscroll和onmousewheel的区别

`onscroll`在被绑定的元素发生滚动时触发，而`onmousewheel`在鼠标滚动时触发，鼠标发生滚动并不意味着不一定被绑定元素发生滚动。

#### onmousewheel和DOMMouseScroll

火狐并不支持`mousewheel`事件，而是监听`DOMMouseScroll`事件。

#### 获取鼠标滚轮的滚动方向

- `event.wheeldelta`，大于0，向上滚
- `event.detail`，小于0，向上滚，兼容火狐。

#### 键盘事件的注意事项

##### 分类

- `keydown`
- `keypress`
- `keyup`

#### `keydown`和`keypress`的区别

- 区别与`keypress`，`keydown`会识别到出字母数字按键外的其他功能键，比如方向键，而`keypress`无法识别。
- 执行顺序不同，键盘按下，`keydown` > `keypress` > `keyup`。

#### 键盘事件属性注意事项

`event.keyCode`和`event.which`要被废弃，推荐使用`event.key`，为按键的字符串。

## BOM的注意事项

### BOM分类

1. `Window`

`window`为全局对象。

2. `Navigator`

包含了浏览器客户端的信息，主要使用`navigator.userAgent`判断浏览器种类。

3. `Location`
4. `History`
5. `Screen`

### 判断浏览器的种类

通过使用`navigator.userAgent`属性和个别浏览器特有的对象来判断浏览器的种类。

```javascript
// 除了ie11无法通过userAgent判断，其他都可以。ie11可以通过特有的ActiveXObject对象来判断

if (navigator.userAgent.search(/chrome/i) !== -1) {
   // Chrome
}
else if (navigator.userAgent.search(/safari/i) !== -1) {
   // Safari
}
else if (navigator.userAgent.search(/opr|opera/i) !== -1) {
   // Opera
}
else if (navigator.userAgent.search(/firefox/i)) {
   // FireFox
}
else if (navigator.userAgent.search(/msie/i)) {
   // IE
}
else if (ActiveXObject) {
   // IE11
}
```

