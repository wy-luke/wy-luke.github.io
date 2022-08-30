---
title: "WPF中获取主窗口 MainWindow 实例，以及在其他窗口中获取 MainWinodw 中的控件"
date: 2022-05-18T15:20:39+08:00
tags: ["WPF","C#"]
---

由于WPF执行的方式有些奇怪，并不是一般意义上的 **“类--实例化”**

所以如果你想要**在其他 Class 文件、或其他窗口中，执行 MainWindow 中的一些函数时**；或者是**想要获取 MainWindow 的某个控件，并对其操作时**（比如你要在一个新的窗口中，改变 MainWindow 的一个 Switch 的开关状态），就非常麻烦

你可以把需要使用的函数定义为 静态（Static），但是这样带来的限制非常多，而且这种方法不适用与获取控件

经查阅，只需一行代码：

```csharp
var _mainWindow = Application.Current.Windows
            .Cast<Window>()
            .FirstOrDefault(window => window is MainWindow) as MainWindow;
```

> Application.Current contains a collection of all windows in your application, you can get the other window with a query such as

然后就可以对 MainWindow 中的任何函数或控件进行操作了，如：

```csharp
_mainWindow.Switch1.IsOn = false;
```

此时函数也无需定义为 静态（Static）了，非常方便。

同理也适用于获取其他窗口，**只需要将上面代码的 MainWindow 改为你需要寻找的窗口名即可**

参考链接:
<https://stackoverflow.com/questions/13644114/how-can-i-access-a-control-in-wpf-from-another-class-or-window/44988191#44988191>
