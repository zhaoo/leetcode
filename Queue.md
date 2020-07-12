### 队列

先进先出 (FIFO)

```javascript
class Queue {
  constructor() {
    this.queue = []
  }
  enQueue(item) {
    this.queue.push(item)
  }
  deQueue() {
    return this.queue.shift()  //使用数组比较消耗性能
  }
  getHeader() {
    return this.queue[0]
  }
  getLength() {
    return this.queue.length
  }
  isEmpty() {
    return this.getLength() === 0
  }
}
```

### 优先级队列

```javascript
class PriorityQueue {
  constructor() {
    this.queue = [{
      priority
      value
    }]
  }
  enQueue(item) {
    if (this.isEmpty()) {
      this.queue.push(item)
    } else {
      var flag = false;  //判断是否排队
      for (let i = this.queue.length - 1; i > 0; i--) {
        if (this.queue[i].priority <= item.priority) {
          this.queue.splice(i, 0, item)
          flag = true
          break
        }
      }
      //循环后未入队，优先级最大，插入到第一位
      if (!flag) {
        this.queue.unshift(item);
      }
    }
  }
}
```

### 循环队列

![设计循环队列](https://leetcode-cn.com/explore/learn/card/queue-stack/216/queue-first-in-first-out-data-structure/865/)

```javascript
var MyCircularQueue = function (k) {
  this.queue = [];
  this.size = k;
  this.head = -1;
  this.tail = -1;
};

MyCircularQueue.prototype.enQueue = function (value) {
  if (this.isFull()) return false;
  if (this.isEmpty()) this.head = 0;
  this.tail = (this.tail + 1) % this.size;
  this.queue[this.tail] = value;
  return true;
};

MyCircularQueue.prototype.deQueue = function () {
  if (!this.isEmpty()) {
    if (this.head === this.tail) {
      this.head = -1;
      this.tail = -1;
    } else {
      this.head = (this.head + 1) % this.size;
    }
    return true;
  }
  return false;
};

MyCircularQueue.prototype.Front = function () {
  return this.head === -1 ? -1 : this.queue[this.head];
};

MyCircularQueue.prototype.Rear = function () {
  return this.tail === -1 ? -1 : this.queue[this.tail];
};

MyCircularQueue.prototype.isEmpty = function () {
  return (this.head === -1 && this.tail === -1);
};

MyCircularQueue.prototype.isFull = function () {
  return ((this.tail + 1) % this.size === this.head);
};

```