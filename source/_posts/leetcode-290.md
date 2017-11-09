---
title: LeetCode#290 Word Pattern - in Swift
date: 2017-11-08 11:47:05
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

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

給定一個字串格式 pattern 和字串 str ，驗證 str 是否符合 pattern 的格式。

Notes:
You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

pattern 字串只包含小寫字母， str 字串包含小寫字母，和用空白分隔段落。

---

# 範例

pattern = "abba", str = "dog cat cat dog" should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog" should return false.
pattern = "abba", str = "dog dog dog dog" should return false.

"dog cat cat dog" 符合 "abba" 的格式，返回 true
"dog cat cat fish" 不符合 "abba" 的格式 ，應為 "abbc" ，返回 false
"dog cat cat dog" 不符合 "aaaa" 的格式，應為 "abba" ，返回 false
"dog dog dog dog" 不符合 "abba" 的格式，應為 "aaaa" ，返回 false

---

# 解題

將 str 用空白切割與 pattern 一同轉為 Array ，如果兩個 Array 不同長度代表不合格式。

開始遍歷兩個陣列各取 p 和 s ，如果 p 已經出現在 hashTable 的 key 裡，查看他的 val 是否與 s 相同，不同就代表不合格式。

如果沒出現過，則查看 s 是否已經出現在 hashTable 的 val 裡，如果有，代表他已經與不同的 key 配對過了，不合格式。

如果上面兩關都通過，將 p 對應 s 加進 hashTable 裡。

遍歷結束都沒有返回 false 代表格式正確。

``` swift
func wordPattern(_ pattern: String, _ str: String) -> Bool {
    if pattern.isEmpty && str.isEmpty { return false }
    let p = Array(pattern)
    let s = str.split(separator: " ")
    var dict = [String : String]()
    if p.count != s.count { return false }
    var i = 0
    while i != p.count {
        if let pre = dict[String(p[i])] {
            if pre != String(s[i]) { return false }
        } else {
            if dict.values.contains(String(s[i])) { return false }
            dict[String(p[i])] = String(s[i])
        }
        i += 1
    }
    return true
}
```
