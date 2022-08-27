---
title: "C++ 自定义排序顺序详解，优先级队列 + lambda 表达式"
date: 2022-03-27T21:41:03+08:00
draft: true
---

## 1. [C++ named requirements ( 具名要求 ) : Compare](https://en.cppreference.com/w/cpp/named_req/Compare)

C++ 中没有 `Comparator` 类，Campare 是一个 `requirement` ，可以理解为一种定义，要求。

>yields `true` if the first argument of the call appears before the second in the strict weak ordering relation induced by this type, and `false` otherwise.

人话来讲，比较两个参数，返回 `bool` 值，当返回 `true` 时，第一个参数排在第二个参数**前面**，即**第一个参数先进入 `Container`**（如 `vector` ）

 注意这里只关心返回 `true` 时的情况， 当两个参数相等（即无排序要求）和第一个参数在后面、第二个参数在前面时，都返回 `false`，在自定义 `Campare` 时需要注意这一点！！！

 也就是说，在自定义 `Campare` 时，当第一个参数排在第二个参数前面时，返回 `true` ，其他情况均返回`false`

所以，在排序时，如果要保持相等元素的相对位置，即稳定排序，要用`stable_sort()`

否则，用`sort()`即可（不能保证相等元素相对位置不变）

## 2. `std::greater` `std::less`

[`std::greater`](https://en.cppreference.com/w/cpp/utility/functional/greater) : 当第一个参数**大于**第二个参数时，返回 `true`

> For T which is not a pointer type, `true` if `lhs > rhs`, `false` otherwise（包括等于时）.
> （ `lhs` 为第一个参数，`rhs` 为第二个参数）

`std::less` 反之

## 3. 排序

对于 `vector` 排序时，若使用 `std::greater`，返回 `true` 时，第一个参数**大于**第二个参数，即较大的数排在前面，先进入 `vector` ，所以排序结果是**降序**

```C++
vector<int> v{ 1, 5, 8, 9, 6, 7, 3, 4, 2, 0 };

// sort 默认为升序，即使用 less<int>() 作为参数
sort(v.begin(), v.end(), greater<int>());
```

对于**优先级队列**，若使用 `std::greater`：当第一个参数**大于**第二个参数时，返回 `true`，即较大的数排在前面，先进入**优先级队列** ，但是 **优先级队列** 为 **先进入的后输出**

>理解：优先级队列想象为**堆**，先进入的在下面，后进入的在上面，遍历时使用 `top()`

所以，排序的结果是较大的数在下面，较小的数在上面，即**小顶堆**

## 4. 使用 lambda 表达式自定义顺序

当容器里面不是 `int` 类型时，就不能直接使用 `greater` 进行排序

此时可以使用  [lambda](https://en.cppreference.com/w/cpp/language/lambda) 表达式，方便地自定义顺序，如：

``` C++
// lambda 表达式作为 Campare，当返回 true 时，left 先进入，后输出，即在优先级队列（堆）的下方
auto cmp = [](pair<int, int> left, pair<int, int> right) -> bool { return left.second < right.second; };
priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> pq(cmp);
```

优先级队列里面存放的是 `pair`，我们定义，当 `left.second < right.second` 时，返回 `true`，即 `second` 值较**小**的排在优先级队列的下方，可以理解为**大顶堆**
