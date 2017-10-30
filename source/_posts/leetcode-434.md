---
title: LeetCode#434 Number of Segments in a String - in Swift
date: 2017-10-25 13:10:25
tags:
- LeetCode
- Swift
- String
categories:
- LeetCode
- Swift
- String
---

# 題目
Count the number of segments in a string, where a segment is defined to be a contiguous sequence of non-space characters.

Please note that the string does not contain any non-printable characters.

算出一個字串中有幾個段落，一個段落代表一段不含空白的連續字元。

注意字串中不計算任何 "沒印出" 的字元

---

# 範例
``` swift
Input: "Hello, my name is John"
Output: 5
```
該字串分為五段，"Hello," 和 "my" 和 "name" 和 "is" 和 "John"

---

# 解題
``` swift
func countSegments(_ s: String) -> Int {
    return s.characters.split(separator: " ").count
}
```

一行解決，用空白字元拆開全部字元，算出拆開的段落有幾個。

