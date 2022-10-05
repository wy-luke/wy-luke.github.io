---
title: "C++ 处理输入"
date: 2022-09-18T17:18:10+08:00
tags: ["C++"]
---

## 1. 输入一个数

```cpp
int a;
cin >> a;
```

## 2. 连续输入一个数

```cpp
int a;
while (cin >> a) {
}
```

## 3. 按行读取

每次读取一行输入，包含空格，已回车换行结束

```cpp
string input;
while (getline(cin, input)) {
}
```

## 4. 按行读取后，提取每行的字符串

- 字符串之间用**空格**间隔

```cpp
string input;
while (getline(cin, input)) {
    istringstream iss(input);
    string str;
    // ">>"会忽视字符串之间所有的回车和空格，即每次读取一个有效字符串输入
    // 在这里 iss 是每行的输入，不包含回车，所以 ">>" 会忽视掉字符串中间的所有空格
    while(iss >> str) {
    }
}
```

- 字符串之间用**逗号**（或其他任意字符）间隔

```cpp
string input;
while (getline(cin, input)) {
    istringstream iss(input);
    string str;
    // 提取分隔符之间的字符串，注意这里提取出的可以是空字符串
    // 若 "a,,b" 则提取出 a b 和一个空字符串
    // 同时，若以间隔符结尾，则不会再记入一个空字符串
    // 若 ",," 则提取出 2 个空字符串
    while(getline(iss, str, ',')) {
    }
}
```
