+++
author = "Abser"
categories = ["leetcode"]
date = 2018-12-09T17:02:34+08:00
description = ""
featured = ""
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "删除链表中的倒数第N个节点"
type = "post"

+++

## 问题描述
给定一个链表，删除链表的倒数第 *n *个节点，并且返回链表的头结点。
### __示例 1__

```plain
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

### __说明__

给定的 *n* 保证是有效的。

### __进阶__

你能尝试使用一趟扫描实现吗？
## 思路
一趟扫描，通过使用两个相距定长 n 的指针，同时向后移动，当后面的指针指到链表的尾部的时候，该指针正好指向需要删除的倒数第 n 个节点
## 实现

### __Go 版本__

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeNthFromEnd(head *ListNode, n int) *ListNode {
	p := &ListNode{Val: 0, Next: head}
	q := p
	qhead := q
	for i := 0; i < n; i++ {
		p = p.Next
	}
	for p.Next != nil {
		p = p.Next
		q = q.Next
	}
	q.Next = q.Next.Next
	return qhead.Next
}
```
### 

