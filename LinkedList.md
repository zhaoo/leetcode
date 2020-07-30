### 反转链表

```javascript
var reverseList = function (head) {
  let pre = null;
  let cur = head;
  while (cur) {
    let next = cur.next;
    cur.next = pre;
    pre = cur;
    cur = next;
  }
  return pre;
};
```

### 删除排序链表中的重复元素

![删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

```javascript
var deleteDuplicates = function (head) {
  var pre = head;
  while (pre && pre.next) {
    if (pre.val === pre.next.val) {
      pre.next = pre.next.next;
    } else {
      pre = pre.next;
    }
  }
  return head;
};
```

### 合并两个有序链表

![合并两个有序链表](https://leetcode-cn.com/explore/featured/card/top-interview-questions-easy/6/linked-list/44/)

> [题解](https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/chun-zhao-wu-yue-ep01mergetwolistshe-bing-liang-ge/)

```javascript
var mergeTwoLists = function (l1, l2) {
  var head = new ListNode();
  var pre = head;
  while (l1 && l2) {
    if (l1.val < l2.val) {
      pre.next = l1;
      l1 = l1.next;
    } else {
      pre.next = l2;
      l2 = l2.next;
    }
    pre = pre.next;
  }
  pre.next = l1 ? l1 : l2;
  return head.next;
};
```

```javascript
if (!l1) return l2;
if (!l2) return l1;
if (l1.val < l2.val) {
  l1.next = mergeTwoLists(l1.next, l2);
  return l1;
} else {
  l2.next = mergeTwoLists(l1, l2.next);
  return l2;
}
```

### 回文链表

![回文链表](https://leetcode-cn.com/explore/featured/card/top-interview-questions-easy/6/linked-list/45/)

```javascript
var isPalindrome = function (head) {
  var pre = head;
  var arr = [];
  while (pre) {
    arr.push(pre.val);
    pre = pre.next;
  }
  while (arr.length > 1) {
    if (arr.pop() !== arr.shift()) {
      return false;
    }
  }
  return true;
};
```

### 环形链表

![环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

```javascript
var hasCycle = function(head) {
  var pre = head;
  while(pre) {
    if(pre.flag) return true;
    pre.flag = true;
    pre = pre.next;
  }
  return false;
};
```

```javascript
var hasCycle = function(head) {
  var slow = head;
  var fast = head;
  while (slow && fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }
  return false;
};
```

### 链表

```javascript
// 节点
function Node (el) {
  this.el = el;
  this.next = null;
}

// 构造函数
function Link () {
  this.head = new Node('head');
}

// 链表结尾追加一个节点
Link.prototype.append = function (el) {
  var currNode = this.head;
  while (currNode.next != null) {
    currNode = currNode.next;
  }
  currNode.next = new Node(el);
}

// 按节点的值查找节点
Link.prototype.find = function (el) {
  var currNode = this.head;
  while (currNode && currNode.el != el) {
    currNode = currNode.next;
  }
  return currNode;
}

// 插入一个节点
Link.prototype.insert = function (newEl, oldEl) {
  var newNode = new Node(newEl);
  var findNode = this.find(oldEl);
  if (findNode) {
    newNode.next = findNode.next;
    findNode.next = newNode;
  } else {
    throw new Error('找不到给定插入的节点');
  }
}

// 展示链表中的元素
Link.prototype.display = function () {
  var currNode = this.head.next;
  while (currNode) {
    console.log(currNode.el);
    currNode = currNode.next;
  }
}

// 寻找给定节点的前一个节点
Link.prototype.findPrev = function (el) {
  var currNode = this.head;
  while (currNode.next && currNode.next.el !== el) {
    currNode = currNode.next;
  }
  return currNode;
}

// 删除给定的节点
Link.prototype.remove = function (el) {
  var prevNode = this.findPrev (el);
  if (prevNode.next != null) {
    prevNode.next = prevNode.next.next;
  } else {
    throw new Error('找不到要删除的节点');
  }
}
```

### 双向链表

```javascript

// 双链表构造函数
function DNode (el) {
  this.el = el;
  this.prev = null;
  this.next = null;
}

function DLink() {
  this.head = new DNode('head');
}

// 在链表结尾添加一个新的节点
DLink.prototype.append = function (el) {
  var currNode = this.head;
  while (currNode.next != null) {
    currNode = currNode.next;
  }
  var newNode = new Node(el);
  newNode.next = currNode.next;
  newNode.prev = currNode;
  currNode.next = newNode;
}

// 根据节点的值查找链表节点
DLink.prototype.find = function (el) {
  var currNode = this.head;
  while (currNode && currNode.el != el) {
    currNode = currNode.next;
  }
  return currNode;
}

// 插入一个节点
DLink.prototype.insert = function (newEl, oldEl) {
  var newNode = new DNode(newEl);
  var currNode = this.find(oldEl);
  if (currNode) {
    newNode.next = currNode.next;
    newNode.prev = currNode;
    currNode.next = newNode;
  } else {
    throw new Error('未找到指定要插入节点位置对应的值！')
  }
}


// 顺序展示链表节点
DLink.prototype.display = function () {
  var currNode = this.head.next;
  while (currNode) {
    console.log(currNode.el);
    currNode = currNode.next;
  }
}

// 查找最后一个节点
DLink.prototype.findLast = function () {
  var currNode = this.head;
  while (currNode.next != null) {
    currNode = currNode.next;
  }
  return currNode;
}

// 逆序展示链表节点
DLink.prototype.dispReverse = function () {
  var currNode = this.head;
  currNode = this.findLast();
  while (currNode.prev != null) {
    console(currNode.el);
    currNode = currNode.prev;
  }
}

// 删除给定的节点
DLink.prototype.remove = function (el) {
  var currNode = this.find(el);
  if (currNode && currNode.next != null) {
    currNode.prev.next = currNode.next;
    currNode.next.prev = currNode.prev;
    currNode.next = null;
    currNode.previous = null;
  } else {
    throw new Error('找不到要删除对应的节点');
  }
}
```

### 循环链表

```javascript
// 循环链表构造函数
function CLink() {
  this.head = new Node('head');
  this.head.next = this.head;
}

// 向循环链表结尾新增一个节点
CLink.prototype.append = function (el) {
  var currNode = this.head;
  while (currNode.next != null && currNode.next != this.head) {
    currNode = currNode.next;
  }
  var newNode = new Node(el);
  newNode.next = currNode.next;
  currNode.next = newNode;
}

// 根据节点的值查找链表节点
CLink.prototype.find = function (el) {
  var currNode = this.head;
  while (currNode && currNode.el != el && currNode.next != this.head) {
    currNode = currNode.next;
  }
  return currNode;
}

// 插入一个节点
CLink.prototype.insert = function (newEl, oldEl) {
  var newNode = new Node(newEl);
  var currNode = this.find(oldEl);
  if (currNode) {
    newNode.next = currNode.next;
    currNode.next = newNode;
  } else {
    throw new Error('未找到指定要插入节点位置对应的值！');
  }
}

// 展示链表元素节点
CLink.prototype.display = function () {
  var currNode = this.head.next;
  while (currNode && currNode != this.head) {
    console.log(currNode.el);
    currNode = currNode.next;
  }
}

// 寻找前一个节点
CLink.prototype.findPrev = function (el) {
  var currNode = this.head;
  while (currNode.next && currNode.next.el !== el) {
    currNode = currNode.next;
  }
  return currNode;
}

// 删除给定的节点
CLink.prototype.remove = function (el) {
  var prevNode = this.findPrev(el);
  if (prevNode.next != null) {
    prevNode.next = prevNode.next.next;
  } else {
    throw new Error('找不到要删除的节点');
  }
}
```