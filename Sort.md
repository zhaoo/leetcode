### 冒泡排序

156.190ms, O(n<sup>2</sup>), O(1), 稳定

```javascript
function bubbleSort(arr) {
  var len = arr.length
  for (var i = 0; i < len; i++)
    for (var j = 0; j < len - i - 1; j++)
      if (arr[j] > arr[j + 1])
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]
  return arr
}
```

### 选择排序

60.689ms, O(n<sup>2</sup>), O(1), 稳定

```javascript
function selectSort(arr) {
  var len = arr.length
  for (var i = 0; i < len; i++) {
    var min = i
    for (var j = i; j < len; j++) {
      min = arr[j] < arr[min] ? j : min
    }
    [arr[i], arr[min]] = [arr[min], arr[i]]
  }
  return arr
}
```

### 快速排序

14.673ms, O(nlog<sub>2</sub>n), O(nlog<sub>2</sub>n), 不稳定

```javascript
function quickSort(arr) {
  if (arr.length <= 1) return arr
  var left = [], right = []
  var pivot = Math.floor(arr.length / 2)
  var pivotValue = arr.splice(pivot, 1)[0]
  for (var i = 0; i < arr.length; i++) {
    if (arr[i] < pivotValue) {
      left.push(arr[i])
    } else {
      right.push(arr[i])
    }
  }
  return [...quickSort(left), pivotValue, ...quickSort(right)]
}
```