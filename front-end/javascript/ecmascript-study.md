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