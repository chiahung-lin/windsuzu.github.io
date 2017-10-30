---
title: LeetCode#9 Palindrome Number - in Swift
date: 2017-10-29 11:07:22
tags:
- LeetCode
- Swift
- Math
categories:
- LeetCode
- Swift
- Math
---

# 題目
Determine whether an integer is a palindrome. Do this without extra space.

驗證一個整數是否為回文。不能使用額外的空間來操作。

---

# 範例

``` swift
Input : 1232332321
Output : True
```
這是一個回文。

``` swift
Input : 1234567
Output : False
```
這不是回文。

---

# 解題

如果將數字做反轉，再比對兩個數字是否一樣，就可以驗證出是否為回文。

但是當你要反轉很大的數字時，有可能造成 overflow 超過整數最大值。

所以其實只需要將數字反轉到一半即可，再確認 half reverse 或是 half reverse 除以 10 是否相等於 half x 。

``` swift
func isPalindrome(_ x: Int) -> Bool {
    if x < 0 || (x > 0 && x % 10 == 0) { return false }
    var x = x
    var half = 0
    
    while x > half {
        half = half * 10 + x % 10
        x /= 10
    }
    return half == x || half / 10 == x
}
```


