+++
author = "Abser"
categories = ["leetcode-middle"]
date = 2018-12-09T16:56:56+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Pow(x,n)"
type = "post"

+++

## 问题描述

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

### __示例 1__
```
输入: [2,3,1,1,4]
输出: true
解释: 从位置 0 到 1 跳 1 步, 然后跳 3 步到达最后一个位置。
```

### __示例 2__
```
输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。
```


## 思路

### 动规
假设位置i(0≤i≤A.length)i(0≤i≤A.length)能够跳跃的最大长度为dp[i]。 
对于数组A = [2,3,1,1,4]， 则有： 
i = 0, dp[0] = A[0] + 0 = 2 
i = 1, if dp[i-1] ≥ i then dp[1] = max{A[1]+1,dp[0]} else dp[1] = 0 
i = 2, if dp[i-1] ≥ i then dp[2] = max{A[2]+2,dp[1]} else dp[2] = 0
类推

### 贪心
Step用来记录从0到第i个位置中所能跳到最远的距离。

## 实现

### 动规
```go
func canJump(nums []int) bool {
    dp := make([]int,len(nums))
    for i:=1;i<len(nums);i++{
        dp[i] = max(dp[i-1],nums[i-1]) - 1
        if dp[i] < 0{
            return false
        }
    }
    
    return dp[len(nums)-1] >=0
}

func max(a int, b int) int{
    if a>b{
        return a
    }
    return b
}
```
### 
### 贪心
```go
func canJump(nums []int) bool {
	if len(nums) == 0 {
		return false
	}
	step := nums[0]
	for i := 1; i < len(nums); i++ {
		if step > 0 {
			step--
			step = max(step, nums[i])
		} else {
			return false
		}
	}
	return true
}

func max(i, j int) int {
	if i >= j {
		return i
	}
	return j
}
```

