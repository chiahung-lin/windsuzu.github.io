---
title: LeetCode#459 Repeated Substring Pattern - in Swift
date: 2017-10-20 14:13:11
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
Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

給定一個不為空的字串，且字元皆為小寫英文字母，字串長度不超過 10000 。
驗證該字串，是否為字串中某子字串複製組合而成。

---

# 範例
Example 1:
``` swift
Input: "abab"
Output: True

Explanation: It's the substring "ab" twice.
```
abab 是被 ab 子字串複製組合而成

Example 2:
``` swift
Input: "aba"
Output: False
```
aba 不為任何子字串的重複

Example 3:
``` swift
Input: "abcabcabcabc"
Output: True

Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
```
abcabcabcabc 為 abc 重組四次， abcabc 重組兩次而成

---

# 解題

若字串符合題目條件，
那字串第一個字元會是每個重複字串的第一個字元(頭)，
而字串最後一個字元會是每個重複字串的最後一個字元(腳)。

將原字串 S 複製為二生出 SS ( abab -> abababab )
再將 SS 頭跟腳去掉得到 S2 ( abababab -> \_bababa\_ )
若在去掉頭腳的 S2 中還可以找到 S 的模式那代表這個字串是符合題目條件的。

``` swift
import Foundation
func repeatedSubstringPattern(_ s: String) -> Bool {
    let ss = s + s
    let s2 = ss.substring(with: ss.index(after: ss.startIndex)..<ss.index(before: ss.endIndex))
    return s2.contains(s)
}
```