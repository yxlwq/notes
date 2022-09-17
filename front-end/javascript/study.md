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

## alert和prompt

alert返回值为undefined,prompt返回值为用户输入的值。

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