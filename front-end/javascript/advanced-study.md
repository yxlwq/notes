# JavaScript的进阶学习笔记

## 数据类型的判断方法

1. typeof

缺陷：
   1. 判断`null`时，会返回`object`。
   2. 判断除函数会返回`function`外，其他对象会返回`object`。

2. instanceof

用于判断该实例对象是否属于该构造函数。

3. 实例.constructor

可直接判断其构造函数。

4. Object.prototype.toString.call

最完美的类型检验方式，会输出`[object 首字母大写的类型字符串]`。

## undefined和null的理解

`undefined`表示未定义，而`null`表示内容为空。

## 变量在内存中存储的形式

1. 栈内存
2. 堆内存

基本类型数据存储在栈内存中，而引用类型会在堆内存中开辟空间存储数据，而在栈内存中保存指向堆内存的指针。因此基本数据类型赋值会得到全新的值，引用数据类型赋值只会得到相同的指针。

## 内存、数据、变量三者关系

内存中存储数据，变量名作为找到该数据存储位置的标识。

## 对象使用时的注意事项

对象作为函数的实参，将指针赋值给形参，形参在对堆内存中的数据修改时，会影响到函数外的对象。

```javascript
let o = {n: 1};
function add1 (x) {
  x.n += 1;
}
add1(o);
console.log(o.n); // 2
```

## 变量对内存的影响

变量有：全局变量、局部变量，数据又可以分为基本类型数据和引用类型数据。全局变量会一直消耗内存，而局部变量里基本类型数据用完立即被释放，引用数据类型如果函数执行完毕后还有使用，就不会被立即释放。

总结：全局变量和在函数外有引用的函数内部变量会不断消耗内存。

```javascript
let num = 1; // 在文档未被刷新前，一直在内存中。
function getAdd1Func () {
  function add1 (x) {
    return x + 1;
  }
  return add1;
}
let add1 = getAdd1Func(); // getAdd1Func执行完毕，由于返回add1函数，add1函数作为函数getAdd1Func的局部变量，不会被立即释放，直至add1函数被执行完毕。
num = add1(num);
```

## 对象属性或方法的引用方式

1. `对象.属性名`
2. `对象[属性名|变量]`

第一种方式的属性名必须满足标识符的命名规则，而第二种方式更加多元化，可以是任意类型数据，好处是可以使用变量，不局限于字符串，并且可以避开标识符的命名规则。

```javascript
let name = 'yxl';
let person = {
  'wq': {
    age: 18,
    sex: '女',
  },
  'yxl': {
    age: 18,
    sex: '男',
  },
  'Jon Jack': {
    age: 18,
    sex: '男',
  },
};
console.log(person[name].sex); // 男，通过变量作为属性名的形式查询
console.log(person['Jon Jack'].sex); // 男，通过该查询方式，可以避开标识符的命名规范
```

注意：**不推荐使用对象作为对象的属性名，因为对象的属性名会自动转换为字符串，而对象通过`toString`来转换为字符串，任何对象都会转为`[object Object]`，从而发生对象取值错误的情况**

## 函数的调用方式

除了正常的调用方式，还可以通过`bind`、`apply`和`call`来调用。

```javascript

let p1 = {
  name: 'yxl',
  like: 'play computer games',
  love() {
    console.log(`${this.name} ${this.like}`);
  },
};

let p2 = {
  name: 'wq',
  like: 'play football',
};

console.log(p1.love());
console.log(p1.love.call(p2));

```

## 回调函数的定义

在函数A中使用函数B作为形参，在外部调用A，传入函数B作为实参，函数B的执行时机由函数内部如何执行该形参来决定，函数B就为回调函数。

## IIFE（Immediately-Invoked Function Expression，立即执行函数）的作用

形成一个封闭的函数的函数作用域，避免产生全局变量，减少内存的浪费。

## 语句末尾是否加分号讨论

可以加可以不加，根据个人的习惯，必须加分号的几种情况：

1. 语句开头为`(`
2. 语句开头为`[`

解决办法：在这两种情况的开头加上一个`;`。