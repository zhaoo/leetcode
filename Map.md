### 集合

```javascript
class Collection {
  constructor(data) {
    this.collection = new Set(data);
  }

  add(data) {
    this.collection.add(data);
  }

  get() {
    return this.collection;
  }

  remove(data) {
    this.collection.remove(data);
  }

  has(data) {
    return this.collection.has(data);
  }

  size() {
    return this.collection.size;
  }

  values() {
    return this.collection;
  }

  union(collection) {
    let arr1 = Array.from(collection);
    let arr2 = Array.from(this.collection);
    return new Set(arr1.concat(arr2));
  }

  intersect(collection) {
    let arr = new Set();
    this.collection.forEach(element => {
      if (collection.has(element)) {
        arr.add(element);
      }
    });
    return arr;
  }

  difference(collection) {
    let arr = new Set();
    this.collection.forEach(element => {
      if (!collection.has(element)) {
        arr.add(element);
      }
    });
    return arr;
  }

  sub(collection) {
    if (this.size() < collection.size()) {
      return false;
    } else {
      let res = true;
      collection.values().forEach(element => {
        if (!this.collection.has(element)) {
          res = false;
        }
      });
      return res;
    }
  }
}
```