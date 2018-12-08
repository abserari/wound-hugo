+++
author = "Abser"
categories = ["leetcode-primary"]
date = 2018-12-08T12:43:36+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "买卖股票的最佳时机-II"
type = "post"

+++

## 问题描述
给定一个数组，它的第 *i* 个元素是一支给定股票第 *i* 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

__注意：__你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

### __示例 1__

```plain
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
```

### __示例 2__

```plain
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

### 示例 3
```plain
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

## 实现
### __Go 版本__

```go
func maxProfit(prices []int) int {
	var max int
	for i := 1; i < len(prices); i++ {
		if prices[i] > prices[i-1] {
			max += prices[i] - prices[i-1]
		}
	}
	return max
}
```
### Go 测试


![image.png | left | 747x161](https://cdn.nlark.com/yuque/0/2018/png/176280/1537953109054-0698b42a-b6ac-4235-9192-366feba1d8df.png "")



![image.png | left | 747x205](https://cdn.nlark.com/yuque/0/2018/png/176280/1537953113578-da2c6049-2f00-44d9-9b85-940783f5c6b8.png "")


![image.png | left | 747x212](https://cdn.nlark.com/yuque/0/2018/png/176280/1537953266976-647c9571-d065-40cf-9594-d1fb795bde45.png "")

