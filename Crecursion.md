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

### N的阶乘（普通递归）

```javascript
function factorial(n) {
  if (n === 0)
    return 1
  return n * factorial(n - 1)
}
```

### N的阶乘（尾递归）

由于普通递归过程中，每次执行都会将调用过程压入`调用栈`中，如果N的技术比较大，可能会栈溢出，所以这里提供尾递归方式解决这个问题。

```javascript
function factorial(n, total = 1) {
  if (n === 0)
    return total
  return factorial(n - 1, n * total)
}
```

注意！在`Node.js`中需要开启`harmony`模式实现尾递归，如下：

```bash
node --harmony_tailcalls factorial.js
```

> [尾递归优化探索](https://github.com/HolyZheng/holyZheng-blog/issues/17)
