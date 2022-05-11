---
title: "实现strStr"
date: 2022-05-11T22:44:48+08:00
lastmod: 2022-05-11T22:44:48+08:00
draft: true
keywords: ["LeetCode"]
description: ""
tags: ["LeetCode"]
categories: ["LeetCode"]
author: ""

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: true
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""
typora-root-url: ..\..\static
---

<!--more-->
# 实现 strStr()

### 题目

> 实现 strStr() 函数。
>
> 给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。
>
> 示例 1:
>
> 输入: haystack = "hello", needle = "ll"
> 输出: 2
> 示例 2:
>
> 输入: haystack = "aaaaa", needle = "bba"
> 输出: -1
> 说明:
>
> 当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。
>
> 对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/implement-strstr
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

---

### 解决方法

+ 好吧，我直接使用了indexOf方法，没救了 T_T

```java
class Solution {
    public int strStr(String haystack, String needle) {
        return haystack.indexOf(needle);
    }
}
```

