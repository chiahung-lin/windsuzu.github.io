---
title: LeetCode#119 Pascal's Triangle II - in Swift
date: 2017-10-24 13:55:01
tags:
- LeetCode
- Swift
- Array
categories:
- LeetCode
- Swift
- Array
---

# 題目
Given an index k, return the kth row of the Pascal's triangle.

給定索引值 k ，返回帕斯卡三角形的第 k+1 層。

---

# 範例
For example, given k = 3,
Return [1,3,3,1].

---

# 解題

首先定義第 k 個的陣列中會有 k + 1 個元素，

如果 k 為 1 直接返回 [1] ， k > 1 則開始從第一層帕斯卡三角形開始組起。

每一層跳過 1 開始，由後往前填滿該層的元素，每個元素恰好為上一層的該元素 + 前一個元素組成。

``` swift
k = 3
res = [1,0,0,0]

第一層
k[1] = k[1] + k[0] = 0 + 1
res = [1,1,0,0]

第二層
k[2] = k[2] + k[1] = 0 + 1
k[1] = k[1] + k[0] = 1 + 1
res = [1,2,1,0]

第三層
k[3] = k[3] + k[2] = 0 + 1
k[2] = k[2] + k[1] = 1 + 2
k[1] = k[1] + k[0] = 2 + 1
res = [1,3,3,1]
```

``` swift
func getRow(_ rowIndex: Int) -> [Int] {
    if rowIndex == 0 { return [1] }
    var res = [Int](repeating: 0, count: rowIndex + 1)
    res[0] = 1
    for i in 1...rowIndex {
        var j = i
        while j >= 1 {
            res[j] += res[j - 1]
            j -= 1
        }
    }
    return res
}
```