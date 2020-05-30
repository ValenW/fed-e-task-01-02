# 王文茏｜Part 1｜模块二

## 简答题

### 第一题

为每个对象维持引用计数器，根据其是否为0判断是不是垃圾

优点：能及时地回收垃圾，最大限度减少程序暂停

缺点：无法回收循环引用对象，需要时刻监视和修改所有对象的引用计数器，时间开销大

### 第二题

0. 通常会通过某些条件触发标记整理，如剩余空间不够等
1. 第一次从根出发遍历所有可达对象，并标记
2. 第二次遍历所有对象，清理未被标记的对象并清除所有标记

### 第三题

1. 内存空间平均分为`from`和`to`两块，活动对象都存放在`from`中
2. 使用标记整理算法清理垃圾，并将剩下的活动对象复制到`to`空间
   1. 复制过程中有可能出现晋升，即将新生代对象转移到老生代空间中
3. 交换`from`和`to`

### 第四题

在老生代垃圾回收的标记阶段使用

工作原理是不一次标记所有活动对象，而是每标记完一层后运行程序，之后再标记下一层对象，这样标记和程序运行穿插进行，直到标记完所有活动对象。类似于分步广度优先遍历

这样就不会因为需要标记的对象太多而影响程序运行，提高了用户体验

## 代码题1

### 练习一

```js
const isLastInStockFlowVersion = fp.flowRight(fp.prop('in_stock'), fp.last)
```

### 练习二

```js
const firstCarName = fp.flowRight(fp.prop('name'), fp.first)
```

### 练习三

```js
const averageDollarValue = fp.flowRight(_average, fp.map(fp.prop('dollar_value')))
```

### 练习四

```js
const sanitizeNames = fp.map(fp.flowRight(_underscore, fp.toLower))
```

## 代码题2

### 练习一

```js
const ex1 = maybe => maybe.map(fp.map(fp.add(1)))._value
```

### 练习二

```js
const ex2 = container => container.map(fp.first)._value
```

### 练习三

```js
const ex3 = user => Maybe.of(user).map(safeProp('name'))._v.map(fp.first)._value
```

### 练习四

```js
const ex4 = n => Maybe.of(n).map(parseInt)._value
```

