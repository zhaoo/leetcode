# 拷贝

基本数据类型: `undefined`，`boolean`，`number`，`string`，`null`, `symbol`

存放在栈内存中的简单数据段，数据大小确定，内存空间大小可以分配，是直接按值存放的，所以可以直接访问。对其进行赋值时，拷贝的是值；修改后它的原始值是不会改变的。

引用类型: `object`, `array`

引用类型是存放在堆内存中的，变量实际上是一个存放在栈内存的指针，这个指针指向堆内存中的地址。每个空间大小不一样，要根据情况开进行特定的分配。对其进行赋值时，拷贝的是地址空间；修改后它的原始值会一起改变。

| — | 和原数据是否指向同一对象 | 第一层数据为基本数据类型 | 原数据中包含子对象 |
| --- | --- | --- | --- |
| 赋值 | 是 | 改变会使原数据一同改变 | 改变会使原数据一同改变 |
| 浅拷贝 | 否 | 改变不会使原数据一同改变 | 改变会使原数据一同改变 |
| 深拷贝 | 否 | 改变不会使原数据一同改变 | 改变不会使原数据一同改变 |

示例对象:

```javascript
const user = {
  name: 'zhaoo',
  gender: 0,
  social: {
    email: 'izhaoo@163.com',
    qq: '894519210',
    wechat: undefined,
  },
  vip: null,
  friendId: [1, 43, 23, 21]
}
```

### 赋值

```javascript
user1 = user
```

### 浅拷贝

##### assign

```javascript
const user1 = Object.assign({}, user)
```

### 深拷贝

##### JSON

```javascript
user1 = JSON.parse(JSON.stringify(user))
```

##### 递归遍历

```javascript
function clone(target) {
  if (typeof target === 'object') {
    let cloneTarget = Array.isArray(target) ? [] : {};
    for (const key in target) {
      cloneTarget[key] = clone(target[key]);
    }
    return cloneTarget;
  } else {
    return target;
  }
};
```

# 防抖节流

### 防抖

在事件频发的情况下，设定一个延迟时间 `n`，`n` 秒后才触发事件；若 `n` 秒内又触发了事件，则重新计算延时。

举个栗子：法师读技能条，延时后开大，技能条会被打断。

```javascript
var debounce = function (fn, delay) {
  var timeout;
  return function () {
    if (timeout) clearTimeout(timeout);
    var ctx = this;
    var args = arguments;
    timeout = setTimeout(function () {
      fn.apply(ctx, args);
    }, delay);
  }
}
```

### 节流

在事件频发的情况下，每隔延迟时间 `n` 才会触发一次事件。

举个栗子：AK射速10发/s

```javascript
var throttle = function (fn, time) {
  var pre = Date.now();
  return function () {
    var self = this;
    var args = arguments;
    var now = Date.now();
    if (now - pre > time) {
      fn.call(self, args);
      pre = Date.now();
    }
  }
}
```

# 手写源码

### call

```javascript
//每个函数有this和args两个默认参数
Function.prototype.myCall = function (context) {
  //传入的对象为空（null,number...）时指定为全局环境
  var context = context || window
  //用this获取调用myCall的函数
  //fn.call(a, 'yck', '24') => this = fn
  context.fn = this
  //args是伪数组，没有slice这个方法
  var args = [...arguments].slice(1)
  //执行并保存结果
  var result = context.fn(...args)
  //删除这个fn对象
  delete context.fn
  //返回结果
  return result
}
```

### apply

```javascript
Function.prototype.myApply = function (context) {
  var context = context || window
  context.fn = this
  var result
  if (arguments[1]) {
    result = context.fn(...arguments[1])
  } else {
    result = context.fn()
  }
  delete context.fn
  return result
}
```

### bind

```javascript
Function.prototype.myBind = function (context) {
  // if (typeof this !== 'function') {
  //   throw new TypeError('Error')
  // }
  var fn = this
  var args = [...arguments].slice(1)
  return function F() {
    if (this instanceof F) {
      return new fn(...args, ...arguments)
    }
    return fn.apply(context, args.concat(...arguments))
  }
}
```

### new

```javascript
function new() {
  let obj = new Object()
  let Constructor = [].shift.call(arguments)
  obj.__proto__ = Constructor.prototype
  let result = Constructor.apply(obj, arguments)
  return typeof result === 'object' ? result : obj
}

function student(name, gender) {
  this.name = name
  this.gender = gender
}

var zhaoo = new(student, 'zhaoo', 'male')
```

1. 创建一个空的简单JavaScript对象（即{}）；
2. 链接该对象（即设置该对象的构造函数）到另一个对象 ；
3. 将步骤1新创建的对象作为this的上下文 ；
4. 如果该函数没有返回对象，则返回this。

# 数组扁平化

### 递归

```javascript
const flat = function (arr) {
  let res = [];
  let len = arr.length;
  for (let i = 0; i < len; i++) {
    if (Array.isArray(arr[i])) {
      res = res.concat(flat(arr[i]));
    } else {
      res.push(arr[i]);
    }
  }
  return res;
}
```

### 字符串

只针对全数字的情况。

```javascript
const flat = function (arr) {
  return arr.toString().split(',').map(item => {
    return Number(item);
  });
}
```

### Reduce

```javascript
const flat = function (arr) {
  return arr.reduce((pre, cur) => {
    return pre.concat(Array.isArray(cur) ? flat(cur) : cur);
  }, []);  //不改变原数组
}
```

# 数组去重

### Set

```javascript
const unique = (arr) => {
  return [...new Set(arr)];
}
```

### indexOf

```javascript
const unique = (arr) => {
  return arr.filter((val, index, arr) => {
    return arr.indexOf(val) === index;
  });
}
```

### 排序

```javascript
const unique = (arr) => {
  return arr.concat().sort().filter((val, index, arr) => {
    return !index || val !=== arr[index - 1];
  })
}
```

# 斐波那契

```javascript
const fibonacci = (n) => {
  if (n <= 2) return 1;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

const fibonacci = (n) => {
  let temp = [1, 1, 1];
  if (n === 1 || n === 2) return 1;
  for (let i = 3; i <= n; i++) {
    temp[i] = temp[i - 1] + temp[i - 2];
  }
  return temp[n];
}
```
