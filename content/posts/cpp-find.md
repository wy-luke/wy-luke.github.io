---
title: "C++ 中的各种 find"
date: 2022-10-05T19:43:51+08:00
tags: ["C++"]
---

C++ 中 `find` 主要分为两种

一种是 `string` 里封装的，只能针对 `string` 搜索，返回类型是 `int` 下标，没搜到时返回 `string::npos`

一种是 `<algorithm>` 里封装的，能对各种东西搜索，返回类型是 `iterator`，没搜到时返回 `end()` 迭代器

## 1. string 中的 find

现有一个 `string s` 搜索目标为 `"abc"`

### [find(string& str, pos = 0)](https://en.cppreference.com/w/cpp/string/basic_string/find)

用法：`s.find("abc")`

Finds the first substring **equal to the given character sequence**. Search begins at pos, i.e. the found substring must not begin in a position preceding pos.

找到**搜索目标**第一次出现的位置，即第一个 `"abc"` 出现的位置

如果搜索目标为空，空字符串第一次出现的位置为字符串开头，即 `s.find(t)` 会返回 0

### [find_first_of(string& str, pos = 0)](https://en.cppreference.com/w/cpp/string/basic_string/find)

用法：`s.find_first_of("abc")`

Finds the first character equal to **one of** the characters in the given character sequence. The search considers only the interval [pos, size()). If the character is not present in the interval, npos will be returned.

找到搜索目标中**任一字符**第一次出现的位置，即第一个 `"a"` 或 `"b"` 或 `"c"` 出现的位置

如果搜索目标为空，即搜索目标中不包含任何字符，所以什么都找不到， `s.find_first_of(t)` 会返回 `npos`

## 2. find

```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <iterator>
 
int main()
{
    std::vector<int> v{1, 2, 3, 4};
    int n1 = 3;
    int n2 = 5;
    auto is_even = [](int i){ return i%2 == 0; };
 
    auto result1 = std::find(begin(v), end(v), n1);
    auto result2 = std::find(begin(v), end(v), n2);
    auto result3 = std::find_if(begin(v), end(v), is_even);
 
    (result1 != std::end(v))
        ? std::cout << "v contains " << n1 << '\n'
        : std::cout << "v does not contain " << n1 << '\n';
 
    (result2 != std::end(v))
        ? std::cout << "v contains " << n2 << '\n'
        : std::cout << "v does not contain " << n2 << '\n';
 
    (result3 != std::end(v))
        ? std::cout << "v contains an even number: " << *result3 << '\n'
        : std::cout << "v does not contain even numbers\n";
}
```

Output:

```c++
v contains 3
v does not contain 5
v contains an even number: 2
```
