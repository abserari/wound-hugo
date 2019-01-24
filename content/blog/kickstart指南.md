+++
author = "Abser"
categories = ["guide"]
date = 2019-01-24T15:43:05+08:00
description = "kickstart使用入门,google"
featured = "pic03.jpg"
featuredalt = "pic03"
featuredpath = "date"
linktitle = ""
title = "Kickstart指南"
type = "post"

+++

# Kick Start快速入门

## Background
Code Jam Kickstart 为同学们提供向 Google 展现自己专业能力以及走近 Google 的机会。在家就可以参加由 Google 的工程师们设计的算法题。通过参加线上测试，同学们可以直观地了解 Google 技术性岗位对编程能力的要求，也是参与 Google 校园招聘的入场券。

## Requirement
* G家邮箱一枚
* 科学上网工具
* [地址传送门](https://codingcompetitions.withgoogle.com/kickstart/archive)（如果从codejam进入的话，选择分类中的kickstart）

## Quickstart-Overview
G家鼓励灵活的解决方案，所以施行的输入输出方案和其他的ACM在线测评不一样。

不是让你不断提交代码然后系统给你测试，而是给你数据集让你自己测试后在本地生成输出文件进行上传。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/176280/1548304826927-983c0662-0022-4203-a838-b45e0b317718.png#align=left&display=inline&height=802&linkTarget=_blank&name=image.png&originHeight=802&originWidth=1433&size=223294&width=1433)<br /><br />
1. 下载题目数据集 `.in` 文件（小数据集4分钟变一次，大数据集8分钟变一次）
1. 解题并生成输出 `.out` 文件
1. 提交输出文件 和 代码源文件（练习测试不用提交）


PS. 每一道题都有小数据集和大数据集两个.in文件可供下载，大数据集的数据范围一般都比小数据集的范围更广，有更多的困难情况。<br /><br />
## [QuickStart](https://codejam.withgoogle.com/codejam/resources/quickstart-guide)
### 必要点    
如果你想参加比赛，请在比赛期间访问你的比赛主页。如果您想练习，请访问“过去的问题”页面并选择一个回合。然后选择一个问题。

读问题，前面几段话将精确描述您的程序需要解决的问题。仔细注意极限部分。这些限制将帮助您确定处理大小数据集所需的解决方案类型。（通常会说明一些无解的数据不用考虑）

编写一个程序，在不到3分钟的时间内用所描述的小限制解决问题。确保您的程序接受输入并以给定的格式输出;如果您使用示例输入作为输入运行它，它应该准确地生成示例输出(包括“Case #”文本)。如果您不确定如何处理输入和输出，请参阅下面的[标准I/O教程](https://www.yuque.com/techcats/guide/enbito#9c961103)，了解可行的做法。

在页面顶部，单击以 `solve A-small`  并下载输入文件。在真正的比赛中，我们一收到下载请求就会启动一个4分钟的计时器。如果你在练习，就不会有计时器。

在该输入文件上运行程序，并将结果保存到文件中。将该文件作为输出文件提交。(在真正的比赛中，你还需要提交你的源代码。)服务器的响应方式有以下几种:

  * 正确示例:您提交的每个案例都完全正确!

  * 拒绝:您的提交被拒绝的原因与您的答案的正确性或不正确性无关。例如，您可能上传了一个输入文件或源代码，而不是您自己的输出文件。时钟仍然在运行，所以需要考虑您能否在超时之前修复这个问题(在这种情况下，您的提交将被视为不正确)。

  * 不正确：**我们不会告诉您哪些情况是错误**较小**的时间惩罚(但是解决问题总比不解决好，即使有惩罚!)

在您解决小数据集之后，大数据集将变得可用。一旦您的程序准备好处理更高的限制，下载大型数据集。(参赛者通常只编写一个解决方案来解决两个数据集。)我们一收到下载请求就会启动一个8分钟的计时器。

与小数据集一样运行程序并提交，直到比赛结束你才知道你是否正确地解决了问题。如果您的提交被拒绝或您想提交另一个答案，您可以在8分钟的时间限制内再次尝试，但只有最后一次提交将被判定。

接着看另一个问题(左边有一个列表)。您正确解出的每个数据集都值下载链接旁边所写的点数。比赛结束时得分最多的选手排名最高。在一个小数据集上，每一次错误的提交最终被正确的回答，将会有4分钟的惩罚时间。为了引人注目，记分牌将显示“乐观”的初步结果,也就是说，它将假设每个大型提交都是正确的。比赛结束后，记分牌将显示真实的结果，包括哪些大的提交是错误的。

### 教程
我们现在只有一个教程，但我们将来可能会添加更多教程。虽然阅读理论很好，但我们强烈建议您练习解决实际问题以使其变得更好。您可以访问我们的 [过去问题](https://codejam.withgoogle.com/codejam/past-contests)部分来完成此操作。For Fun！

#### “标准”解决方案：使用标准输入和输出
Kickstart鼓励灵活解决问题：我们会为您提供输入文件，并让您以自己喜欢的方式解决问题。您可以选择语言，开发环境，体系结构，库等。

我们的许多参赛者使用其他编程竞赛中常见的模型，如ACM-ICPC和Codeforces：一个单文件程序，它读取输入并准确生成所需的输出。本教程演示如何使用标准输入和标准输出将此模型应用于Kickstart！当然，仍然欢迎您以完全不同的方式阅读输入和/或写入输出; 这只是一个选择。

#### 什么是标准输入和标准输出？
标准输入（stdin）和标准输出（stdout）是程序用于与外界交互的数据流。当您以最简单的方式从控制台运行程序时，stdin就是从键盘读入程序的内容，而stdout就是打印在屏幕上的内容。但是，这两个流可以被定向读取和写入文件！

假设您有一个名为“my_program”的程序，通常通过以下命令运行：<br />`MY_PROGRAM`<br />请注意，如果使用像C语言++编译为机器码，`MY_PROGRAM`可能是这样的<br />`./my_binary`<br />，对于像Java使用虚拟机，<br />`java my_java_binary_name`<br />或者像Python这样的解释型语言<br />`python my_python_code.py`<br />在Linux，Mac OS / X和Windows中，您可以使用<和>将stdin和stdout分别重定向到文件。

命令行如下
```powershell
MY_PROGRAM < input_file.txt > output_file.txt
```

将使您的程序接收`input_file.txt`其stdin中的内容，并将输出写入其stdout `output_file.txt`。

#### 如何在Kickstart中使用stdin和stdout？

在处理解决方案时，您可能希望从文件中读取（例如，`sample.txt`您已将问题的样本I / O复制到其中），但想要把输出写入控制台。你可以这样做：
```powershell
MY_PROGRAM < sample.txt
```

下载输入后，您需要将输出定向到要上载的文件：
```powershell
MY_PROGRAM < small_input.txt > small_output.txt
```

如果程序的算法适用于Small和Large数据集，则只需重新运行此命令，甚至不需要更改或重新编译程序：
```powershell
MY_PROGRAM < large_input.txt > large_output.txt
```

#### 如何编写我的代码以从stdin读取并写入stdout？
考虑以下非常简单的问题。输入一个 **T ，T **N **M**。所需的输出形式是`Case #x: y z`，在这里`x`， `y`和`z`均为整数; `x`是的第 x 个情况，`y`是的**M**N**的总和，并且`z`是产品**N**M**。

input_file.txt
```powershell
3
1 5
7 -2
9001 0
```
这里有一些代码来解决这个问题，从stdin读取并以各种语言写入stdout。对于我们的示例，我们使用了Kickstart中一些最常用的语言，但您当然不仅限于使用这些语言！

C ++（命令行）
```powershell
g++ solution.cpp -o solution
./solution < input_file.txt > output_file.txt
```

C ++（solution.cpp）
```cpp
#include <iostream>  // includes cin to read from stdin and cout to write to stdout
using namespace std;  // since cin and cout are both in namespace std, this saves some text
int main() {
  int t, n, m;
  cin >> t;  // read t. cin knows that t is an int, so it reads it as such.
  for (int i = 1; i <= t; ++i) {
    cin >> n >> m;  // read n and then m.
    cout << "Case #" << i << ": " << (n + m) << " " << (n * m) << endl;
    // cout knows that n + m and n * m are ints, and prints them accordingly.
    // It also knows "Case #", ": ", and " " are strings and that endl ends the line.
  }
  return 0;
}
```

Java（命令行）
```powershell
javac Solution.java
java Solution < input_file.txt > output_file.txt
```

Java（Solution.java）
```java
import java.util.*;
import java.io.*;
public class Solution {
  public static void main(String[] args) {
    Scanner in = new Scanner(new BufferedReader(new InputStreamReader(System.in)));
    int t = in.nextInt();  // Scanner has functions to read ints, longs, strings, chars, etc.
    for (int i = 1; i <= t; ++i) {
      int n = in.nextInt();
      int m = in.nextInt();
      System.out.println("Case #" + i + ": " + (n + m) + " " + (n * m));
    }
  }
}
```

Python 2（命令）
```powershell
python2 solution.py < input_file.txt > output_file.txt
```

Python 2（solution.py）
```python
# raw_input() reads a string with a line of input, stripping the '\n' (newline) at the end.
# This is all you need for most Kickstart problems.
t = int(raw_input())  # read a line with a single integer
for i in xrange(1, t + 1):
  n, m = [int(s) for s in raw_input().split(" ")]  # read a list of integers, 2 in this case
  print "Case #{}: {} {}".format(i, n + m, n * m)
  # check out .format's specification for more formatting options
```

Python 3（命令）
```powershell
python3 solution.py < input_file.txt > output_file.txt
```

Python 3（solution.py）
```python
# input() reads a string with a line of input, stripping the '\n' (newline) at the end.
# This is all you need for most Kickstart problems.
t = int(input())  # read a line with a single integer
for i in range(1, t + 1):
  n, m = [int(s) for s in input().split(" ")]  # read a list of integers, 2 in this case
  print("Case #{}: {} {}".format(i, n + m, n * m))
  # check out .format's specification for more formatting options
```
从这些示例中可以看出，大多数语言提供了从stdin读取和写入stdout的简单方法。这通常比直接引用代码中的特定文件更容易 - 从Small数据集切换到Large数据集时，或者从控制台切换输出目标（用于调试）时，无需更改或重新编译代码一个文件（所以你可以提交一样的源文件）。

您可以随时查看您喜欢的语言的文档，以找到使用stdin和stdout的首选方法。几乎所有语言都有一个。
