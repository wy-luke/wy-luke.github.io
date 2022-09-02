---
title: "Python中列表截取（Slice，即冒号 : ）的用法详解"
date: 2021-07-13T22:20:32+08:00
tags: ["python"]
---

## 1. 基本用法

```python
a[start:stop]  # 从 index=start 开始（即包含start），到 index=stop-1（即不包含stop）
a[start:]      # 从 index=start 开始（包含 start ），到最后
a[:stop]       # 从头开始，到 stop-1
a[:]           # 取整个 List
```

**注意**：

1. **结束的 `index` （索引值）** 是 `stop-1` ，也就是说**不**包含 `index=stop` 的那个值
2. 我这里说的 `index` 是索引值，从 0 开始，这个大家应该都知道

```python
a[1:4]  # 从 index=1 取到 index=4
a[1:]   # 从 index=1 取到最后
```

```python
a[n, start:stop]   # 对一个二维 List，取第 n 行，从 index=start 到 index=stop-1 间的列
```

具体示例：

```python
>>> a = [1,2,3,4,5,6]
>>> a[1:4]
[2, 3, 4]

>>> a[1:]
[2, 3, 4, 5, 6]
```

## 2. 步长 step

除此之外，还有一个 `step` （步长）的东西：

```python
a[start:stop:step]  # 从 index=start 到 index=stop-1，每隔 step 取一个，不超过 stop-1
```

具体示例：

```python
>>> a = [1,2,3,4,5,6]
>>> a[::2]  # 注意这个双冒号就是省略了 start 和 stop，即从头取到尾，每隔 2 步取一个
[1,3,5]
```

注意：

1. `step` 默认为1
2. `stop` 和 `start` 的差就是截取片段的长度（当 `step` 是1时）

## 3. index 为负数时

`start` or `stop` 也可以为负数，就意味着从后往前数：

```python
a[-1]    # 取最后一个值
a[-2:]   # 取最后两个值
a[:-2]   # 取除最后两个值之外的所有值
```

具体示例：

```python
>>> a = [1,2,3,4,5,6]
>>> a[-1] 
[1,3,5]
```

## 4. step 为负数时

同样的，`step`也可以取负数，当`step`为负数时，发生了一点小变化
`step`为负数代表`从后往前`取，这时`start > stop`，也就是说 `start` 是较后面的数，`stop` 为前面的数
和上面一样，`start`包含，`stop`不包含
具体示例：

```python
>>> a = [1,2,3,4,5,6]
>>> a[3:1:-1]
[4, 3]

>>> a[1::-1]
[2, 1]
```

好好理解一下

## 5. 常见错误

1. 当你截取的范围 **完全** 超过数组的长度时，你会得到一个空列表，而 Python 不会报错。
比如：当 `a` 仅包含 1 个元素，而你使用 `a[5:]`  `a[:-2]`  时，你就会得到一个空列表，而不是报错信息，这点尤其需要注意。

2. 当你截取的范围 **部分** 超过数组的长度时，你会得到你截取到的部分，而 Python 不会报错。
比如：

```python
>>> a = [1]
>>> a[:5]
[1]

>>> a[-5:]
[1]
```

## 6. 记忆技巧

```python
 +---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1   0
```

> One way to remember how slices work is to think of the indices as pointing between characters, with the left edge of the first character numbered 0. Then the right edge of the last character of a string of n characters has index n.
>
> 如上图所示，你把 `start` 和 `stop` 想象成是指向两个元素**之间**的，而不是指向元素。这样显然，`start` 和 `stop` 之间的元素，就是你截取的片段。
