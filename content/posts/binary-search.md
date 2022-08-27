---
title: "C++ STL 二分 lower_bound / upper_bound 用法详解"
date: 2022-05-25T14:44:19+08:00
tags: ["算法", "C++", "STL"]
---

假设我们要在一个 `vector<int>` 中，查找一个数 `value`

## 语法

```C++
auto p = std::lower_bound(v.begin(), v.end(), value)
auto p = std::upper_bound(v.begin(), v.end(), value)
```

返回的值类型是 `iterator` 即迭代器，理解为指针即可

## 定义

[`lower_bound`](https://en.cppreference.com/w/cpp/algorithm/lower_bound) 获取第一个**大于等于**`value`的指针
> is not less than

[`upper_bound`](https://en.cppreference.com/w/cpp/algorithm/upper_bound) 获取第一个**大于** `value`的指针
> is greater than value

## 用法详解

由上可以引申出多种用法：

1. 要查找的每个数都存在时，如果这个数只存在一次
`lower_bound` 和 `upper_bound  - 1` 结果一样，同样指向该数，`upper_bound` 指向第一个大于`value`的数

2. 要查找的每个数都存在时，如果这个数存在**多次**
`lower_bound` 能查找到左侧边界，`upper_bound  - 1` 能查找到右侧边界

3. 要查找的数不在时
`lower_bound` 和 `upper_bound` 结果一样，同样指向第一个大于`value`的数

## 引申

STL 里面还有一个 `equal_range()`，就是返回一个`pair`，分别为 `lower_bound` 和 `upper_bound` 的结果

可以理解为一个左闭右开 `[start, end)` ，区间为要查找的 `vector` 里面，等于 `value` 的部分

为什么呢，因为 `lower_bound` 找到第一个**等于**（如果存在） `value` 的，`upper_bound` 找到第一个**大于** `value` 的，所以中间的部分，自然就是等于 `value` 的部分

## 手写二分

若**左闭右开**区间，则 `while (l < r)`

若**左闭右闭**区间，则 `while (l <= r)`

全部 `return left`

当寻找 `lower_bound` 时，向左侧靠拢，left 即为 `lower_bound`，即第一个大于 `val` 的

当寻找 `upperr_bound` 时，向右侧靠拢，left 即为 `upper_bound`，即第一个大于 `val` 的
