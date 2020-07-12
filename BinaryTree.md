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