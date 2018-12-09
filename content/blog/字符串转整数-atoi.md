+++
author = "Abser"
categories = ["leetcode-middle"]
date = 2018-12-09T16:50:05+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "字符串转整数 Atoi"
type = "post"

+++

## 问题描述

请你来实现一个 `atoi` 函数，使其能将字符串转换成整数。

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。

__说明：__

假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−2^31^,  2^31 ^− 1]。如果数值超过这个范围，qing返回  INT\_MAX (2^31 ^− 1) 或 INT\_MIN (−2^31^) 。

### __示例 1__

```
输入: "42"
输出: 42
```

### __示例 2__

```
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
```

### __示例 3__

```
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
```

### __示例 4__

```
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
```

### __示例 5__

```
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

## 思路
注意越界即可

## 实现
```go
const (
	MAX int32 = 1<<31 - 1
	MIN int32 = -1*MAX - 1
)

func myAtoi(str string) int {
	if len(str) == 0 {
		return 0
	}
	runes := []rune(str)
	var ret int32
	var neg bool
	i := 0
	for ; i < len(runes) && runes[i] == rune(' '); i++ {
	}
	if i == len(runes) {
		return 0
	}
	if runes[i] == rune('-') || runes[i] == rune('+') {
		neg = runes[i] == rune('-')
		i++
	}

	for ; i < len(runes); i++ {
		if val, ok := toInt(runes[i]); !ok {
			break
		} else {
			if neg {
				if -ret < (MIN+val)/10 {
					return int(MIN)
				}
			} else {
				if ret > (MAX-val)/10 {
					return int(MAX)
				}
			}
			ret = 10*ret + val
		}
	}
	if neg {
		return int(-ret)
	}
	return int(ret)
}

func toInt(r rune) (int32, bool) {
	ret := int32(r - rune('0'))
	if ret >= 0 && ret <= 9 {
		return ret, true
	}
	return 0, false
}
```
### 


