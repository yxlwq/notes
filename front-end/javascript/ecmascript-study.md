# ECMAScript的学习笔记

## var和let的区别

- var存在变量提升，let由于存在TDZ（Temporal Dead Zone，暂时性死区），因此无法在let声明之前对变量进行访问。
- var可以重复声明变量，let只能声明同一个变量一次，且之前如果以使用var或者let声明，会报错。
- var声明的变量是函数作用域，而let声明的变量是块级作用域。

## const的使用注意事项

- const声明的是常量，在初始化时就必须赋值。
- const声明的变量的值不可以在改变，但如果赋的值是对象，由于赋值的是指针，因此只是指针不能改变，而指针指向的数据可以被改变。
- const声明的变量的作用域是块级作用域。
  
## const赋值为对象的问题

单纯赋值对象，对象的内容是可以改变的，只是不可以改变指针，可以通过使用`Object.freeze`方法来冻结对象，使得对象内容不可以再修改。

## 解构赋值的注意事项

### 解构会沿着原型查找

对对象和数组进行解构时，自身没有的属性，会沿着原型链进行查找。

### 默认值

避免没有值时，数组和对象解构得到`undefined`。

```javascript
let oldArr = [];
let [a = 2] = oldArr; // 2
let oldObj = {};
let {b = {c: 1}} = oldObj; // {c: 1}
```

### 将剩余数据赋值给变量

使用剩余模式，可以将剩余的数据收集起来。

```javascript
let arr = [1, 2, 3, 4, 5];
let [, ...newArr] = arr; // [2, 3, 4, 5]
let obj = {a: 1, b: 2, c: 3};
let {a, ...newObj} = obj; // {b: 2, c: 3}
```
### 对象解构赋值

对象不声明进行解构赋值，需要给`{}`加上`()`，否则`{}`会被认为是代码块。

### 给新变量命名并提供默认值

```javascript
let obj = {a: 1};
let {a:a2 = 0, b: b2 = 0} = obj; // a2：1,b2：0
```

### 函数参数的默认值

```javascript
function func({a = 'a', b = {b2: 1}} = {}) {}
```

### 解构嵌套的对象和数组

```javascript
let obj = {
  arr: [1,true, {
    arr: [1, 2, 3], // 获取这个
  }],
  obj: {
    a: 1,
    arr: [1, 2, {
      obj: {
        a: 1,// 获取这个
      },
    }],
  }
};
let {
  arr: [,,{
    arr:newArr // [1, 2, 3]
  }],
  obj: {
    arr: [,, {
      obj: {
        a: newA // 1
      }
    }],
  }
} = obj;
```

### for...of中的解构

在`for...of`中，可以对其参数进行解构。

```javascript
// 解构数组
let arr = [
  ['k1', 'v1'],
  ['k2', 'v2'],
  ['k3', 'v3'],
];
for(let [key, value] of arr) {
  console.log(key, value);
}

// 解构对象
let person = [
  {
    name: 'p1',
  },
  {
    name: 'p2',
  },
  {
    name: 'p3',
  },
];
for(let {name} of person) {
  console.log(name);
}
```

### 解构函数的实参

```javascript
function getHobby({hobby}) {
  console.log(hobby);
};
let man = {
  name: 'm1',
  hobby: 'like to play football',
};
getHobby(man); // like to play football
```

### 动态解构对象的属性

```javascript
let hobby = {
  'p1': 'h1',
  'p2': 'h2',
};
function getHobby(hobby, who) {
  ({[who]: who} = hobby);
  console.log(who);
}
```

### 解构无效的标识符

```javascript
let obj = {
  'o-bj': 1,
};
let {
  'o-bj': newName, // 1
} = obj;
```

## 模板字符串的注意事项

### 作用

1. 嵌入变量
2. 可以换行

```javascript
let data = 1
let html = `<p>
              <span>${data}</span>
            </p>`;
```

### 自定义模板字符串的注意事项

1. 通过自定义标签函数来达到自定义模板字符串的输出。

```javascript
function toggleCase(str, module = 'lower') {
  str = str.join('');
  return module == 'lower' ? str.toLowerCase() : module === 'upper' ? str.toUpperCase() : str;
}
console.log(toggleCase`ABCDE`);
console.log(toggleCase`${'upper'}ABCDE`);
console.log(toggleCase`${'lower'}ABCDE`);
```

2. 标签函数的第一个参数是个伪数组，该参数有个属性为`raw`为包含了原始的字符串的数组。

```javascript
function tag(str) {
  console.log(str.raw[0]);
}
let str = tag`test one \n test two`; // test one \n test two
```

3. String.raw方法和原始模板字符串作用一致

```javascript
let a = 1;
let b = 2;
let str;
str = `${a} + ${b} = ${a + b}`;
// 等价于
str = String.raw`${a} + ${b} = ${a + b}`;
```

## 对象书写的简化

1. 属性的简化

```javascript
let name = 'yxl';
let hobby = function () {};
let person = {
  name, // 简化,
  hobby,
};
```

2. 方法的简化

```javascript
let person = {
  name: 'yxl',
  hobby(){}, // 简化
};
```

## 箭头函数的注意事项

### 特点

- 箭头函数没有自己的this,在函数被定义时会向外层寻找最近的this。

```javascript
let obj = {
  x: 1,
  y: 1,
  output() {
    let add = () => this.x + this.y;
    return add();
  },
};
console.log(obj.output()); // 2
```

- this找到后，不可以使用`bind|call|apply`改变。

```javascript
let obj = {
  x: 1,
  y: 1,
  output() {
    let add = () => this.x + this.y;
    return add.call(obj2);
  },
};
let obj2 = {
  x: 2,
  y: 2,
}
console.log(obj.output()); // 2
```

- 可以简化函数的写法。

### 函数简化

```javascript
// 只有一个参数
x => {};

// 没有参数
() => {};

// 函数体只有返回值
() => 1;

// 只有一个参数，且只有返回值
x => x + 1;
```

## `...`的作用

1. 收集参数

```javascript
function addTotal(...num) { // 收集参数
  return num.reduce((l, r) => l + r);
}
addTotal(1,2,3,4); // 10
```

2. 分散参数

```javascript
let obj = {a: 1, b: 2};
let newObj = {...obj}; // 分散参数，浅拷贝对象
```

3. 利用收集参数的作用代替`arguments`

## Symbol的注意事项

### Symbol的特点

- 独一无二
- 不能参与计算
- for...in不能获取到Symbol属性名，可以使用`Reflect.ownkeys`获取。

### Symbol的创建

1. Symbol
2. Symbol.for

Symbol.for会维护一张key/value表，因此`Symbol.for('key') === Symbol.for('key')`得到的是同一个值，为true。

```javascript
let symbol = Symbol('symbol');
symbol = Symbol.for('symbol');
```

### Symbol上的一些特殊属性的作用

用来自定义JavaScript中原始的行为。

### 访问Symbol数据的字符串

```javascript
console.log(Symbol('字符串').description); // '字符串'
```

## 迭代器是什么？

迭代器又称迭代器对象，是一个包含`next`方法的对象，next方法会返回包含`value`和`done`的对象，当`done`为`true`时，迭代完成。

## Iterator的作用

自定义迭代行为，且使得对象这些不可迭代的数据结构可以进行迭代。

```javascript
let obj = {
  a: 1,
  b: 2,
  c: 3,
  d: 4,
  /*
  也可以这样写：
  *[Symbol.iterator]() {
    // 函数体
  },
  */
};
obj[Symbol.iterator] = function *() {
  let keys = Object.keys(obj);
  let values = Object.values(obj);
  for(let i = 0; i < keys.length; i++) {
    yield [keys[i], values[i]];
  }
};
for(let [key, value] of obj) {
  console.log(key, value);
}

function * test() {
  console.log('初始化');
  let x1 = yield 'ok';
  let x2 = yield x1 + 1;
  yield '结束';
};
```

## 生成器的注意事项

生成器是一个函数，执行后可以返回一个迭代器对象，可以通过`yield`将函数分成不同的执行片段，`yield`可以返回`value`的值和接收`next`函数传回的值。生成器的定义形式：

```javascript
function *genAdd(x = 0) {
  let total = x;
  let y = 0;
  console.log('开始加法运算');
  while(true) {
    y = yield total;
    if(y < 0) break;
    total += y;
  }
  console.log('结束加法运算')
  return total;
}
let total = 0;
let add = genAdd(total);
add.next(); // '开始加法运算'
add.next(1);
add.next(2);
add.next(4);
total = add.next(-1).value; // '结束加法运算'
console.log(total); // 7
```

## Promise的注意事项

### Promise的作用

由于通过不断嵌套回调函数来处理异步请求的方式会产生回调地狱，对代码维护不友好，Promise被设计处理，Promise可以链式调用的特点解决了回调地狱的缺点。

### Promise的创建

Promise是一个构造函数，通过实例化构造函数可以得到promise对象。

```javascript
function readFile(success = true) {
  return new Promise(function (resolve, reject) {
    setTimeout(() => {
      if(success) resolve('ok');
      else reject('读取错误');
    },3000);
  });
};
readFile(false).catch(err => console.log(err));  // 读取错误
```

### Promise的理解

promise对象有三个状态：pendding（等待）、fullfilled（成功）、rejected（失败）。通过给Promise构造函数传入处理异步的函数，函数传入两个函数参数来决定promise之后的状态，`resolve`函数执行后状态变为`fullfilled`，`reject`函数执行后状态变为`rejected`，未执行前状态为`pendding`。promise对象有一个`then`方法，用于注册成功或失败后用于处理的回调函数，有两个参数，第一个是成功的回调，第二个是失败的回调，在promise对象状态变为`rejected`或者`fullfilled`后执行。由于then方法会返回promise对象，因此可以继续链式调用`then`方法。promise对象还有`catch`和`finally`方法，同样可以链式调用，`catch`用于接收处理失败的回调函数，用于解决每个then都要传入失败的回调函数的情况，`finally`会不管成功或失败都执行。

### catch和finally的理解

```javascript
// catch理解
let fn = () => {};
Promise.reject().catch(fn);
/* 等价于：
Promise.reject().then(null, fn);
*/

// finally
Promise.resolve().finally(fn);
/* 等价于
Promise.resolve().then(fn, fn);
*/
```

### Promise.all、any、race、allSettled的区别

- `Promise.all`，全部promise成功后，状态变为成功，有一个失败就失败，类似逻辑关系与。
- `Promise.any`，全部promise失败后，状态变为失败，有一个成功就成功，类似逻辑关系或。
- `Promise.race`，状态跟随最开始变化的那个promise的状态。
- `Promise.allSettled`，所有promise的状态都改变后，调用自身的`fullfilled`回调函数。

[具体区别](https://juejin.cn/post/6948277034304929799)

## Set的注意事项

### Set的特点

集合的元素不会从重复。

### Set常用的方法和属性

- `size`，类似数组的length属性。
- `add`，添加元素。
- `delete`，删除元素。
- `has`，查找元素是否存在。
- `clear`，清空数据。

### Set和Array之间的转换

```javascript
let s = new Set(1,2,2,3,4,4); // 1, 2, 3, 4
let arr = [1, 2, 2, 3, 4, 4];
// Set => Array
console.log([...s]);
console.log(Array.from(s));

// Array => Set
console.log(new Set(arr));
```

## Map的注意事项

## Map的结构

Map实际上是一个存放`[key, value]`的数组。

### Map和Object的优缺点

Map的优点：

- 可使用`for...of`和`...`。
- 属性名可以使用任何数据类型，没有限制。

Object的优点：

- 可以直接key对应value,查询速度快。

### Map常用的属性和方法

- `size`，同Set。
- `delete`，同Set。
- `clear`，同Set。
- `set`，用于设置key和value。
- `get`，同Set的`has`。

## class的注意事项

### class的特点
class的新语法只是一个语法糖，和传统的构造函数一样，也是利用原型链实现特定的功能。

### class和传统构造函数写法的差异

```javascript
// 构造函数位置
// 传统写法
function Cls() {
  // 构造函数函数体
}
// class写法
class Cls {
  constructor() {
    // 构造函数函数体
  }
}

// 向原型添加属性
// 传统写法
function Cls() {}
CLs.prototype.func = () =>  {}; // 向原型上添加方法
// class写法
class Cls {
  func() {}; // 向原型上添加方法
}

// 向构造函数本身添加属性
// 传统写法
function Cls() {}
CLs.func = () =>  {}; // 添加静态方法
// class写法
class Cls {
  static func() {}; // 添加静态方法
}

// 向实例添加实例属性
// 传统写法
function Cls() {
  this.func = () =>  {}; // 添加实例方法
}
// class写法
class Cls {
  num = 0; // 添加实例属性
  constructor() {
    this..func = () =>  {}; // 添加实例方法
  }
}
```

### class和构造函数的继承的区别

```javascript
// 传统构造函数继承
function ClsA(a) {
  this.a = a;
}
ClsA.prototype.func = () => {};
ClsA.funcB = () => {};
function ClsB(a, b) {
  ClsA.call(this, a); // 1. 继承ClsA的实例属性
  this.b = b;
}
for(let key in ClsA) { // 2. 继承ClsA的静态属性
  ClsB[key] = ClsA[key];
}
Object.setPrototypeOf(ClsB.prototype, ClsA.prototype); // 3. 继承ClsA原型上的属性
let cls = new ClsB(1,2);
console.log(cls.a, cls.func, ClsB.funcB);

// class继承
class ClsA {
  constructor(a) {
    this.a = a;
  }
  func() {};
}
ClsA.funcB = () => {};
class ClsB extends ClsA { // 第一步
  constructor(a, b) {
    super(a, b); // 第二步
  }
}
let cls = new ClsB(1,2);
console.log(cls.a, cls.func, ClsB.funcB);
```

### super关键字的作用

super是一个只读的关键字。

- 作为函数使用。

在构造函数中首先调用super方法，完成继承。

```javascript
class ClsA {
  constructor(a) {
    this.a = a;
  }
}
class ClsB extends ClsA {
  constructor(a, b) {
    super(a);
    this.b = b;
  }
}
```

- 作为对象使用

  1. 在非静态方法中使用，等价于父类的原型对象。

  ```javascript
  class ClsA {
    func() {
      console.log('func');
    };
  }
  class ClsB extends ClsA {
    funcB() {
      super.func();
    }
  }
  let cls = new ClsB();
  cls.funcB();
  ```

  2. 在静态方法中使用，等价于父类。

  ```javascript
  class ClsA {
    static func() {
      console.log('func');
    }
  }
  class ClsB extends ClsA{
    static funcB() {
      super.func();
    }
  }
  ClsB.funcB();
  ```

### 私有属性的注意事项

#### 私有属性、公有属性和保护属性的区别

- 私有属性，只能在自身类中使用，无法在外部和子类中使用。
- 保护属性，只能在自身类中和子类中使用，无法在外部使用。
- 公有属性，可以在任何地方使用。

#### 私有属性的使用

```javascript
class Cls {
  #x;
  constructor(x) {
    this.#x = x;
  }
  callX() {
    console.log(this.#x);
  }
}
```

## getter和setter的注意事项

### getter和setter的理解

getter和setter相当于一个拦截器，拦截对象或类的属性，getter拦截读取操作，setter拦截设置操作。利用getter和setter可以自定义对象属性的默认行为。

### getter和setter的使用场景

在类或对象中使用。

```javascript
// 对象
let obj = {
  a: 1,
  get A() {
    console.log('读取obj.a的值');
    return this.a;
  },
  set A(newA) {
    console.log('重新设置obj.a的值');
    this.a = newA;
  },
};
console.log(obj.A);
obj.A = 2;

// class
class Cls {
  a = 1;
  get A() {
    console.log('读取obj.a的值');
    return this.a;
  }
  set A(newA) {
    console.log('重新设置obj.a的值');
    this.a = newA;
  }
}
let cls = new Cls();
console.log(cls.A);
cls.A = 2;

// 给类本身添加
class Cls {}
Cls.a = 1;
Object.defineProperty(Cls, 'A', {
  get() {
    console.log('读取Cls.a的值');
    return Cls.a;
  },
  set(newA) {
    console.log('重新设置Cls.a的值');
    Cls.a = newA;
  },
});
console.log(Cls.A);
Cls.A = 2;
```

## Math.trunc、Math.floor的区别

正数时，没有区别，负数时，区别如下：

```javascript
let num = -1.4;
console.log(Math.floor(num)); // -2
console.log(Math.trunc(num)); // -1
```

## Number.EPSILON作用

`Number.EPSILON`表示一个误差，两个浮点数之差小于`Number.EPSILON`则相等，否则不相等。

## Object.is的作用

用于比较两个数是否相等，解决了`NaN == NaN`为`false`的问题。

## Object.assign的作用

对象合并，将其他参数和并到第一个参数，是前拷贝。

## 设置获取原型

1. `Object.getPrototypeOf`，获取对象原型
2. `Object.setPrototypeOf`，设置对象原型

## 模块化的优势

- 防止变量命名冲突
- 代码复用
- 可维护性好

## 模块化规范分类

1. ES模块化规范

[ES模块化详解](https://juejin.cn/post/6844904003722018830)

2. CommonJS模块化规范

[CommonJS和ES模块化详解](https://juejin.cn/post/6994224541312483336)

3. AMD模块化规范
4. CMD模块化规范

## async/await的理解

[async/await理解](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function)

## Object.create方法使用

创建一个指定原型和属性的对象，第一个参数是原型，第二个参数是描述属性的对象。

```javascript
let obj = Object.create(Object.prototype, {
  a: {
    value: 1,
    /*
      默认不可遍历、不可修改、不可删除
      enumerable: false,
      configurable: false,
      writable: false,
    */
    // 
  },
  b: {
    value: {
      c: 1,
    }
  }
});
```

## 正则的常见问题

### 命名分组

```javascript
let str = 'yxl like to eat apple.';
let {man, fruit} = str.match(/^(?<man>\w+).+?(?<fruit>\w+)\.$/).groups;
console.log(man, fruit);
```

### 断言分类

1. 正向断言
2. 反向断言

```javascript
let str = 'abc555';
// 正向断言
console.log(/[A-z]+(?=\d+)/.test(str));

//反向断言
console.log(/(?<=[A-z]+)\d+/.test(str));
```

### dotAll模式

在正则表达式中`.`用于匹配除换行符以外的字符。

## match、matchAll和g匹配模式的注意事项

- match，匹配到一个直接返回数组，加上全局匹配模式g后，返回匹配到的字符串数组。
- matchAll，匹配多个，返回结果数组，相当于多个match不断执行的结果组成的数组，必须加上全局匹配模式g。

## Array.from、Object.fromEntries和Object.entries的区别

- `Array.from`，将伪数组转为数组。
- `Object.entries`，将对象转为`[key, value]`为组成单位的数组。
- `Object.fromEntries`，将`[key, value]`为组成单位的数组转为对象。

## trim、trimStart/trimLeft、trimEnd/trimRight的使用

- `trim`，将两侧空白删除。
- `trimEnd`和`trimRight`，将右侧空白删除。
- `trimStart`和`trimLeft`，将左侧空白删除。

## flat和flatMap的区别

- flat用于平铺数组一次。
- flatMap，相当于先map后flat

```javascript
let arr = [[1],[2],[[3]]];
console.log(arr.flat()); // [1,2,[3]]
arr = [1,2,3,4];
console.log(arr.map(it => [it])); // [[1],[2],[3],[4]]
arr = [[1],[2],[[3]]];
console.log(arr.flatMap(it => it)); // [1,2,3,4]
```

## 可选链操作符

在不确定对象属性的情况下，如果在对象不存在的属性，上继续取属性，会报错，而可选链操作符就会将这情况从报错变为返回`undefined`，从而避免程序报错。

```javascript
function getUserName() {}; // 异步取值
let result = getUserName() || {}; // 需要取到user.name属性，但是不确定user是否存在
// 使用可选链操作符，避免错误发生
console.log(result?.user?.name); //虽然不存在，但是只返回undefined,不报错
```

## 动态导入模块的注意事项

在ESModule中，由于JavaScript使用静态分析，因此import必须定义在开头，而动态导入模块的引入，支持import在运行时使用。动态import函数返回的是一个Promise对象。

```javascript
// method.js
export {
  getUserData() {
    // 异步方法，根据用户名获取用户数据
  },
}

// 获取用户数据的页面，在异步获取到用户名后，再导入getUserData方法
getUserName().then(async name => {
  let {getUserData} = await import('method.js');
  let data = await getUserData(name);
  // 其他操作
});
```

## BigInt的注意事项

### 使用BigInt的原因

在JavaScript中有一个最大安全整数为`Number.MAX_SAFE_INTERGATER`，当对大于最大安全数进行运算时，会出现运算结果不精准问题，因此BigInt类型数据诞生。

### BigInt的使用

BigInt只能是整数，当用BigInt函数转换浮点数时，会报错，BigInt类型数据只能和BigInt类型数据做运算，以及字符串做加法运算，如果其他类型数据做运算会报错。

```javascript
123n + '' // '123'
123n + 123 // error
123n + true // error
...
123n == 123 // true
123n === 123 // false
```

### globalThis使用的原因

在不同的宿主环境中，表示全局变量的标识符不同，如：
- 浏览器中：this、self来表示window全局对象。
- nodeJS中：this来表示global全局对象。

为保证在不同的宿主环境中，对全局变量的标识符保持一致，出现了`globalThis`，它在不同的宿主环境中都表示当前环境的全局变量。
