### 数组结构转树

```javascript
const transformTree = (list) => {
  const tree = [];
  list.forEach(item => {
    if (item.pid === '0') {
      const children = queryChildren(item, list);
      tree.push(children);
    }
  });
  return tree;
}

const queryChildren = (parent, list) => {
  const tree = [];
  list.forEach(item => {
    if (item.pid === parent.id) {
      const children = queryChildren(item, list);
      tree.push(children);
    }
  });
  if (tree.length) {
    parent.children = tree;
  }
  return parent;
}
```