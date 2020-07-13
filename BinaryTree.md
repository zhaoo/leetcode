### 二叉树的最大深度

```javascript
var maxDepth = function (root) {
  if (!root) return 0;
  let leftDeep = maxDepth(root.left);
  let rightDeep = maxDepth(root.right);
  let maxDeep = Math.max(leftDeep, rightDeep);
  return maxDeep + 1;
};
```

### 二叉树的最小深度

```javascript
var minDepth = function (root) {
  if (!root) return 0;
  let queue = [root];
  let deep = 0;
  while (queue.length) {
    deep++;
    let len = queue.length;
    while (len--) {
      const node = queue.shift();
      if (!node.left && !node.right) return deep;
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
  }
};
```

### 验证二叉搜索树

```javascript
var isValidBST = function (root) {
  let max = -Number.MAX_VALUE;
  let flag = true;
  const inOrder = function (node) {
    if (node) {
      inOrder(node.left);
      node.val > max ? max = node.val : flag = false;
      inOrder(node.right);
    }
  }
  inOrder(root);
  return flag;
};
```

### 对称二叉树

```javascript
var isSymmetric = function (root) {
  const symmetric = function (p, q) {
    if (!p && !q) return true;
    if (!p || !q) return false;
    if (p.val != q.val) return false;
    return symmetric(p.left, q.right) && symmetric(p.right, q.left)
  }
  return symmetric(root, root);
};
```

### 二叉树的层序遍历

```javascript
var levelOrder = function (root) {
  let res = [];
  if (!root) return res;
  const recursion = function (node, level) {
    if (res.length == level) res.push([]);
    res[level].push(node.val);
    if (node.left) recursion(node.left, level + 1);
    if (node.right) recursion(node.right, level + 1);
  }
  recursion(root, 0)
  return res;
};
```

```javascript
var levelOrder = function (root) {
  let res = [];
  if (!root) return res;
  let queue = [root];
  let level = 0;
  while (queue.length) {
    res.push([]);
    let len = queue.length;  //注意缓存
    for (let i = 0; i < len; i++) {
      node = queue.shift();
      res[level].push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    level++;
  }
  return res
};  
```

### 将有序数组转换为二叉搜索树

```javascript
var sortedArrayToBST = function (nums) {
  if (nums.length === 0) return null;
  if (nums.length === 1) return new TreeNode(nums[0]);
  const mid = Math.floor(nums.length / 2);
  const root = new TreeNode(nums[mid]);
  root.left = sortedArrayToBST(nums.slice(0, mid));
  root.right = sortedArrayToBST(nums.slice(mid + 1));
  return root;
};
```