+++
author = "Abser"
categories = ["leetcode"]
date = 2018-12-09T16:58:30+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "打家劫舍III"
type = "post"

+++

## 问题描述

在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

### __示例 1__

```
输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
```

### __示例 2__

```
输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
```

## 思路

### 回溯
每一个根节点讨论是否选与不选，比较左右孩子节点值之和 和 没有左右孩子节点之和，选取大的计入
<span data-type="color" style="color:rgb(73, 73, 73)"><span data-type="background" style="background-color:rgb(255, 255, 255)">这种方法重复计算了很多地方，比如要完成一个节点的计算，就得一直找左右子节点计算，</span></span>消耗时间过多

所以使用一个 map 存储已经算过的节点

## 实现

### 回溯

```go
func rob(root *TreeNode) int {
	m := make(map[*TreeNode]int)
	return dfs(root, m)
}

func dfs(root *TreeNode, m map[*TreeNode]int) int {
	if root == nil {
		return 0
	}
	if m[root] != 0 {
		return m[root]
	}

	val := 0

	if _, ok := m[root]; !ok {
		if root.Left != nil {
			val += dfs(root.Left.Left, m) + dfs(root.Left.Right, m)
		}

		if root.Right != nil {
			val += dfs(root.Right.Left, m) + dfs(root.Right.Right, m)
		}
		m[root] = max(root.Val+val, dfs(root.Left, m)+dfs(root.Right, m))
		return m[root]
	}
	return 0
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```
### 

