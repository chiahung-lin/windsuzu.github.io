---
title: LeetCode#205 Isomorphic Strings - in Swift
date: 2017-11-02 14:18:09
tags:
- LeetCode
- Swift
- Hash Table
categories:
- LeetCode
- Swift
- Hash Table
---

# 題目

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

給定兩個字串 s 和 t ，驗證他們是否同構。

兩個字串要達成同構， s 字串比需要能被 t 完全取代。

完全取代指的是每一個被取代的字元，可以被自己本身取代，但不能有一個字元被兩個以上不同字元取代的狀況發生。

Note:
You may assume both s and t have the same length.

你可以假設 s 和 t 為相同長度。

---

# 範例

``` swift
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.
```

---

# 解題

定義一個 Dictionary 記錄 s 每個字元對應的 t 字元

如果是 "abc" 對應 "xyz" 即是 ["a": "x", "b": "y", "c": z]

如果字典中存在 s 字元對應的值，就比對是否和當下的 t 字元相等。
比對不同，則返回 false 。

如果字典中不存在，那就找出字典中是否有 value 已經存在 t 字元。
已存在，則返回 false 。
不存在，字典中新增一筆 s 對應 t 的記錄。

如果跑完迴圈，都沒發生問題，返回 true 。

``` swift
func isIsomorphic(_ s: String, _ t: String) -> Bool {
    var dict = [Character: Character]()
    let s = Array(s.characters)
    let t = Array(t.characters)
    
    for i in 0..<s.count {
        if let pre = dict[s[i]] {
            if pre != t[i] { return false }
        } else {
            if dict.values.contains(t[i]) { return false }
            dict[s[i]] = t[i]
        }
    }
    return true
}
```