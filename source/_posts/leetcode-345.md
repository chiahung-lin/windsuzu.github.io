---
title: LeetCode#345 Reverse Vowels of a String - in Swift
date: 2017-10-17 15:25:58
tags:
- LeetCode
- Swift
- Two Pointers
- String
categories:
- LeetCode
- Swift
- Two Pointers
- String
---

# 題目
Write a function that takes a string as input and reverse only the vowels of a string.

反轉字串，但只反轉母音的部分。

---

# 範例
``` swift
Example 1:
Given s = "hello", return "holle".
```

hello 中的 eo 轉換為 oe

``` swift
Example 2:
Given s = "leetcode", return "leotcede".
```

leetcode 中的 eeoe 轉換為 eoee

---

# 解題

定義母音表，接著像 [Reverse String](https://windsuzu.github.io/leetcode-344/) 這題一樣進行兩個指針的迴圈。

不同的是，若當下左邊的字母不為母音，就將左指針 +1
反之，右邊不為母音，將右指針 -1

確定抓到左右兩個母音時，就將左右調換，左右各進退一步。

``` swift
func reverseVowels(_ s: String) -> String {
    let set: Set<Character> = ["a", "e", "i", "o", "u", "A", "E", "I", "O", "U"]
    var s = Array(s.characters)
    var left = 0
    var right = s.count - 1
    while left < right {
        while left < right && !set.contains(s[left]) {
            left += 1
        }
        while left < right && !set.contains(s[right]) {
            right -= 1
        }
        let temp = s[left]
        s[left] = s[right]
        s[right] = temp
        left += 1
        right -= 1
    }
    return String(s)
}
```
