+++
author = "Abser"
categories = ["leetcode"]
date = 2018-12-09T16:57:36+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "移动K位数字"
type = "post"

+++

## 问题描述

给定一个以字符串表示的非负整数 *num*，移除这个数中的 *k *位数字，使得剩下的数字最小。

__注意:__

* *num* 的长度小于 10002 且 ≥ *k。*
* *num* 不会包含任何前导零。

### __示例 1 __

```
输入: num = "1432219", k = 3
输出: "1219"
解释: 移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219。
```

### __示例 2 __

```
输入: num = "10200", k = 1
输出: "200"
解释: 移掉首位的 1 剩下的数字为 200. 注意输出不能有任何前导零。
```

### 示例__ 3 __

```
输入: num = "10", k = 2
输出: "0"
解释: 从原数字移除所有的数字，剩余为空就是0。
```

## 思路
贪心
## 实现

### 
```go
func removeKdigits(num string, k int) string {
    digits := len(num) - k
    stack := make([]byte,len(num))
    top := 0
    for i := range num {
        for top > 0 && stack[top-1] > num[i] && k > 0 {
            top--
            k--
        }
        stack[top] = num[i]
        top++
    }
    i := 0
    for i < digits && stack[i] == '0' {
        i++
    }
    if i == digits {
        return "0"
    }
    return string(stack[i:digits])
}
```

