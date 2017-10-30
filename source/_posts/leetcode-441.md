---
title: LeetCode#441 Arranging Coins - in Swift
date: 2017-10-27 13:18:18
tags:
- LeetCode
- Swift
- Math
- Binary Search
categories:
- LeetCode
- Swift
- Math
- Binary Search
---

# 題目
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

給你 n 個硬幣排成樓梯的形狀，每 k 層有 k 個硬幣。

現在給你 n ， 返回你最大可以排成的樓梯有幾層。 n 為一個非負數整數。

---

# 範例
Example 1:
``` swift
n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
```
5 個硬幣排完第 3 層還沒完成，所以返回 2 。

Example 2:
``` swift
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
```
8 個硬幣排完第 4 層還沒完成，所以返回 3 。

---

# 解題

## Iterative

對 n 從第一層開始減，直至無法再減。
代表該層未完成，返回前一層的值。

``` swift
func arrangeCoinsIterative(_ n: Int) -> Int {
    var n = n
    for i in 1...Int.max {
        if n - i >= 0 {
            n -= i
        } else {
            return i - 1
        }
    }
    return 0
}
```

## Mathematic

要算出 n 層的硬幣有幾個，等於要算出 1 + 2 + 3 + ... + n 

這有一個公式是(上底+下底)乘高除以2 : `sum = (1 + x) * x / 2`

並且在這題裡面的 sum 要小於等於 n ， 所以為 `(1 + x) * x / 2 <= n`

解出這個式子 :
> (1 + x) \* x / 2 <= n
x^2 + x  <= 2n
4x^2 + 4x <= 8n
(2x + 1)(2x + 1) - 1 <= 8n
x <= (√(8n + 1) - 1) / 2

``` swift
import Foundation
func arrangeCoinsMathematic(_ n: Int) -> Int {
    return Int((sqrt(8 * Double(n) + 1) - 1) / Double(2))
}
```