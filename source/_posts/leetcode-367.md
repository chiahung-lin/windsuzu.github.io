---
title: LeetCode#367 Valid Perfect Square - in Swift
date: 2017-10-18 14:39:48
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
Given a positive integer num, write a function which returns True if num is a perfect square else False.

給一正整數，驗證其是否為一個完全平方數。

Note: Do not use any built-in library function such as sqrt.

不使用任何語法中的 sqrt 函式。

---

# 範例
Example 1:
``` swift
Input: 16
Returns: True
```
16 可以是 4 的平方數


Example 2:
``` swift
Input: 14
Returns: False
```
14 不是任何正整數的平方數

---

# 解題

# 解法一
根據 http://www.cs.wustl.edu/~kjg/CS101_SP97/Notes/SquareRoot/sqrt.html 的指引，要達成 sqrt function 的運作，首先先找出一個數符合 `y^2 = x, y = x/y` ，知道這個條件後:

* 猜一個數 g 來代表 y ，並且測試
* 檢驗 x / g
* 如果 x/g 等於 g ，那就代表找到 sqrt 的解，若沒有等於，再猜一個更好的 g
* 這個更好的 g 等於 x 和 x /g 的平均值

``` swift
func isPerfectSquare(_ num: Int) -> Bool {
    var x = num
    while x * x > num {
        x = (x + (num/x)) / 2
    }
    return x * x == num
}
```

# 解法二
使用二元搜尋法，從對半開始找起，如果等於答案則返回 true 。

大於則將右邊改為中間數 - 1，小於則將左邊改為中間數 + 1 。持續對半搜尋答案。

``` swift
func isPerfectSquareBinary(_ num: Int) -> Bool {
    var (left, right) = (1, num)
    while left <= right {
        let mid = (left + right) / 2
        if mid * mid == num {
            return true
        } else if mid * mid > num {
            right = mid - 1
        } else {
            left = mid + 1
        }
    }
    return false
}
```




