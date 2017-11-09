---
title: LeetCode#20 Valid Parentheses - in Swift
date: 2017-11-06 20:19:58
tags:
- LeetCode
- Swift
- String
- Stack
categories:
- LeetCode
- Swift
- String
- Stack
---

# 題目

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

給一個字串，裡面只會包含 `'('`, `')'`, `'{'`, `'}'`, `'['` , `']'` ，現在驗證字串是否符合格式。

這些括號，必須要按照正確的順序合起來， `"()"` 或 `"()[]{}"` 就是正確的，但 `"(]"` 或 `"([)]"` 就不是。

---

# 範例

Example 1:
``` swift
Input : "({})"
Output : True
```
這是正確的括號開始跟結尾的用法。

Example 2:
``` swift
Input: "{{]}"
Output: False
```
這是錯誤的括號用法。

---

# 解題

這題題目提示是一題 Stack 的題目， Swift 雖然沒有 Stack 類別 ，但 Array 也有提供 popLast 的用法。

只要遇到三種括號的開頭，就將該括號的結尾加進陣列中

若遇到三種括號的結尾時，陣列為空代表根本沒出現過開頭，回傳 false 。

若陣列的 popLast 回傳的第一個元素，不等於自己，代表開頭不對稱，也回傳 false 。

最後若跑完字串，陣列被 pop 到空的，就是一個 valid 的字串，回傳 true 。

``` swift
func isValid(_ s: String) -> Bool {
    let s = Array(s)
    var stack = [String]()
    
    for c in s {
        switch c {
        case "(":
            stack.append(")")
        case "{":
            stack.append("}")
        case "[":
            stack.append("]")
        default:
            if stack.isEmpty { return false }
            if let pop = stack.popLast(), pop != String(c)   {
                return false
            }
        }
    }
    return stack.isEmpty
}
```