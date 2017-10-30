---
title: LeetCode#172 Factorial Trailing Zeroes - in Swift
date: 2017-10-26 14:27:22
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
Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.

給定整數 n ，返回 n! 中有幾個後綴的 0 。

---

# 範例

Example 1 :
``` swift
Input: 5!
Output: 1
```
5! = `1 * 2 * 3 * 4 * 5` = 120
後綴有 1 個 0 所以回傳 1

Example 2 :
``` swift
Input: 25!
Output: 6
```
25! = 15511210043330985984000000
後綴共有 6 個 0 所以回傳 6

---

# 解題
從 `5!` 看為什麼會有後綴的 `0`
因為 `1 * 2 * 3 * 4 * 5` 有 `2` 跟 `5` 相乘得出 `10`
但從 `1` 到 `n` 那麼多個 `2` ，真正造成後綴出現 `0` 的是 `5`
所以我們只需要對 `n / 5` 即可

但 `25!` 不是 `25 / 5 = 5` 嗎，為什麼是 `6`
因為 `25` 本身還多包含了 `5 * 5` ，所以要 + 1

這邊利用遞迴若 `n / 5` 還可以被 `5` 除，那就在加進原來的答案中

``` swift
func trailingZeroes(_ n: Int) -> Int {
    return n == 0 ? 0 : n / 5 + trailingZeroes(n / 5)
}
```
