---
title: Leetcode |哈希表
tags: 数据结构
categories:
  - 天天向上
description: leetcode 哈希表题解。
abbrlink: 24289
date: 2022-08-20 06:06:15
---

**模板题**

[LC383.赎金信](https://leetcode.cn/problems/ransom-note/)

---

[LC49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/)

> 结合例题的[LC242.有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)。将一个单词的所有字母进行重新排列得到新的单词，那我们可以将每个单词按照一定顺序排列后的值，作为关键码，相同的放到一起，就想到了用哈希表实现。

[LC438.找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string)

> 注意如果p长度大于s，那么一定没有结果，直接返回。
>
> 然后记录p数组的字母构成数量。维护一个滑动窗口。当前的字母数量小于0维护左边界。最好当前窗口长度等于p长度时，记录左边界。
