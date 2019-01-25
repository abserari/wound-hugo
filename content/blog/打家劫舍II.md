+++
author = "Abser"
categories = ["leetcode"]
date = 2018-12-09T16:58:37+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "打家劫舍II"
type = "post"

+++


## 问题描述

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都__围成一圈，__这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，__如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警__。

给定一个代表每个房屋存放金额的非负整数数组，计算你__在不触动警报装置的情况下，__能够偷窃到的最高金额。

### __示例 1__

```
输入: [2,3,2]
输出: 3
解释: 你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。
```

### __示例 2__

```
输入: [1,2,3,1]
输出: 4
解释: 你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

## 思路
分两种情况讨论，数组第一个偷的情况和第一个不偷的情况

## 实现

### 方法一

```go
func rob(nums []int) int {
	switch size {
	case 0:
		return 0
	case 1:
		return nums[0]
	}

	m := make([]int, 2)
	m[0] = nums[0]
	m[1] = max(nums[0], nums[1])
	for i := 2; i < len(nums)-1; i++ {
		m = append(m, max(m[i-1], m[i-2]+nums[i]))
	}

	n := make([]int, 2)
	nums[0] = 0
	n[0] = nums[0]
	n[1] = max(nums[1], nums[0])
	for j := 2; j < len(nums); j++ {
		n = append(n, max(n[j-1], n[j-2]+nums[j]))
	}

	return max(m[len(nums)-2], n[len(nums)-1])
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```
### 

