+++
author = "Abser"
categories = ["leetcode-middle"]
date = 2018-12-09T16:52:40+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Z字形变换"
type = "post"

+++

## 问题描述
将字符串 `"PAYPALISHIRING"` 以Z字形排列成给定的行数：

```
P   A   H   N
A P L S I I G
Y   I   R
```

之后从左往右，逐行读取字符：`"PAHNAPLSIIGYIR"`

实现一个将字符串进行指定行数变换的函数:

```
string convert(string s, int numRows);
```

### __示例 1__

```
输入: s = "PAYPALISHIRING", numRows = 3
输出: "PAHNAPLSIIGYIR"
```

### __示例 2__

```
输入: s = "PAYPALISHIRING", numRows = 4
输出: "PINALSIGYAHRPI"
解释:

P     I    N
A   L S  I G
Y A   H R
P     I
```

## 思路

### 方法一
按照与逐行读取 Z 字形图案相同的顺序访问字符串。
首先访问 `行 0`中的所有字符，接着访问 `行 1`，然后 `行 2`，依此类推...
对于所有整数 k，
* `行 0` 中的字符位于索引`k(2⋅numRows−2)` 处;
* `行 numRows−1 `中的字符位于索引 `k(2⋅numRows−2)+numRows−1` 处;
* 内部的` 行 i` 中的字符位于索引`k(2⋅numRows−2)+i` 以及` (k+1)(2⋅numRows−2)−i `处;

### 方法二
通过从左向右迭代字符串，确定字符位于 Z 字形图案中的哪一行。
使用min(numRows,len(s)) 个列表来表示 Z 字形图案中的非空行。
从左到右迭代 s，将每个字符添加到合适的行。可以使用当前行和当前方向这两个变量对合适的行进行跟踪。
只有当向上移动到最上面的行或向下移动到最下面的行时，当前方向才会发生改变。

## 实现

### 方法一

```go
func convert(s string, numRows int) string {
    if ( len(s) == 0 || len(s) == 1 ||numRows == 1 || len(s) <= numRows){
		return s
	}
	result := make([]byte,0, len(s))
	for i := 0; i < numRows; i++{
		result = append(result, s[i])
		for j := i; j < len(s) ; {
			if 	j += 2 * (numRows - i  - 1);j < len(s)&& numRows - i  - 1 != 0{
				result = append(result, s[j])
			}
			j += 2 * i
			if j < len(s) && i != 0 {
				result = append(result, s[j])
			}
		}
	}
	return string(result[:])
}
```
### 
### 方法二
```go
func convert(s string, numRows int) string {
    if numRows == 1 || len(s) <= numRows {
		return s
	}

	res := bytes.Buffer{}
	p := numRows*2 - 2

	for i := 0; i < len(s); i += p {
		res.WriteByte(s[i])
	}

	for r := 1; r <= numRows-2; r++ {
		res.WriteByte(s[r])

		for k := p; k-r < len(s); k += p {
			res.WriteByte(s[k-r])
			if k+r < len(s) {
				res.WriteByte(s[k+r])
			}
		}
	}

	for i := numRows - 1; i < len(s); i += p {
		res.WriteByte(s[i])
	}
```

