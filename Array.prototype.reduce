# Array.prototype.reduce()

## 概述
>*reduce()* 方法接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始缩减，最终为一个值

## 语法
```arr.reduce([callback, initialValue])```

## 参数
### callback
执行数组中每个值的函数，包含四个参数:
#### previousValue
上一次调用回调函数返回的值，或者是提供的初始值（initialValue）
#### currentValue
数组中当前被处理的元素
#### currentIndex
当前被处理元素在数组中的索引, 即currentValue的索引.如果有initialValue初始值, 从0开始.如果没有从1开始.
#### array
调用 reduce 的数组
#### 返回 
当前累积的值

### initialValue
可选参数, 作为第一次调用 callback 的第一个参数。

## 返回值
最后一次调用回调函数返回的结果


## 描述
reduce 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：
* previousValu 上一次值
* currentValue 当前值
* currentIndex 当前值的索引
* array 数组

1. 回调函数第一次执行时，previousValue 和 currentValue可能是两个不同值其中的一个;
2. 如reduce有initialValue参数，那么previousValue等于initialValue，并且currentValue等于数组中的第一个值;
3. 如reduce没有initialValue参数，那么previousValue等于数组中的第一个值, currentValue等于数组中的第二个值。

## 示例
### 数组累加
```
// reduce 只有一个参数，初始值为arr的第一个值1
let arr = [1, 2, 3, 4, 5];
arr.reduce((pre, cur) => pre + cur);
// out 15
```
```
// reduce 只有一个参数，初始值为reduce的第二个参数2
let arr = [1, 2, 3, 4, 5];
arr.reduce((pre, cur) => pre + cur, 2);
// out 17
```

### 扁平话一个二维数组
```
[[0, 1], [2, 3], [4, 5]].reduce((a, b) => a.concat(b), []);
```
