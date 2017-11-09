---
title: LeetCode#507 Perfect Number - in Swift
date: 2017-11-05 22:20:01
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

We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself.

Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not.

我們定義一個「完美數」是一個正整數，且他的全部因數除了自己本身，加起來等於他自己。

現在給你一整數 n ，寫出一個函式驗證該數是否為完美數。

---

# 範例

``` swift
Input: 28

Output: True

Explanation: 28 = 1 + 2 + 4 + 7 + 14
```

28 的全部因數有 1, 2, 4, 7, 14, 28 ，排除 28 ，其他加起來又等於 28 ，所以返回 true

---

# 解題

先求 num 的所有因子，由於 1 為每個數的因子，所以將 1 先加進 sum 裡面

判斷 s 的因子只需要從範圍 [2, sqrt(num)] 下手，判斷這個範圍內的 i 是否可以被 num 整除

如果可以整除，代表 i 和 num/i 都是 num 的因子，加進 sum 中

最後判斷 sum 是否等於 num 即可

``` swift
import Foundation
func checkPerfectNumber(_ num: Int) -> Bool {
    if num <= 1 { return false }
    
    var sum = 1, i = 2, s = Int(sqrt(Double(num)))
    while i <= s {
        if num % i == 0 { sum += i + (num / i) }
        i += 1
    }
    
    return sum == num
}
```