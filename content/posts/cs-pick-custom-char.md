---
title: "C# 正则表达式匹配特定字符然后做任意处理，并保留字符位置"
date: 2021-12-15T15:47:37+08:00
tags: ["C#"]
---

针对稍简单的操作，一行代码即可搞定

```C#
string text = "abcabc";

// Regex.Replace 的第一个参数为要处理的字符串，第二个为正则表达式，第三个为你的操作
// 匹配字符串中所有的 a，然后转为大写。m.Value 即为匹配到的字符
text = Regex.Replace(text, "[a]", m => m.Value.ToUpper());

Console.WriteLine(text);

>>>"AbcAbc"
```

针对更复杂的操作，可以专门写一个函数

```C#
private static string ReplaceMethod(Match m)
{
 // m.ToString() 即为匹配到的字符，可做任意处理
    return m.ToString().ToUpper();
}

private static void Main()
{
    var text = "abcabc";
    
    var myEvaluator = new MatchEvaluator(ReplaceMethod);
    text = Regex.Replace(text, "[a]", myEvaluator);
    
    Console.WriteLine(text);
}

>>>"AbcAbc"
```
