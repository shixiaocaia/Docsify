---
title: Leetcode |链表
tags: 数据结构
categories:
  - 天天向上
description: leetcode 链表题解。
abbrlink: 30258
date: 2022-08-09 14:06:15
---

## LEETCODE 例题

**[LC203.移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)**

> 使用C++，注意释放删除的内存空间。

**[LC707.设计链表](https://leetcode.cn/problems/design-linked-list/)**

> 思路简单，但是全是细节的题。
>
> 模拟了链表的各种操作。

**[LC206.反转链表](https://leetcode.cn/problems/reverse-linked-list/)**

> 方法1：递归
>
> 递归的方法与双指针的方法相同，简洁一些。
>
> 方法2：双指针

**[LC24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)**

> 通过循环判断后两个节点是否为空
>
> ![24.两两交换链表中的节点1](http://pic.shixiaocaia.fun/202208110712982.png)
>
> 1. 保存后两个节点
> 2. cur 指向 2 这个节点
> 3. 再指向1这个节点
> 4. 最后指向下一组的3

**[LC19.删除链表的倒数第N个节点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)**

> 处理数组、链表中的某部分——双指针
>
> 将fast指针指向删除节点的前一个节点，然后fast指针遍历到NULL时，刚好slow指针遍历到要删除的节点。
>
> 同样用哑节点，规避了分类头节点问题。

**[面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)**

> 先计算两个链表的长度，计算他们长度差，将指针移动到统一起点。
>
> 开始遍历较长的链表（默认A，比较后交换），当二者指针相同相等时，找到了相交节点返回，否则返回NULL。
>
> 注意判断交点是**指针相等**，不是数值相等。

**[LC142.环形链表II](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)**

> 待做，主要是涉及到的数学问题。
>
> 1. 判断是否有环形
> 2. 判断环形的入口

## 归纳总结

- 链表的例题第一遍都是参考的思路，涉及指针的操作，是过去不熟悉的，需要多次复习。
- 增加**哑节点**可以使得处理头节点像其他非头节点情况下。
- 节点的大小，和数组一样从0开始。