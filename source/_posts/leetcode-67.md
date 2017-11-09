---
title: LeetCode#67 Add Binary - in Swift
date: 2017-11-09 13:56:18
tags:
- LeetCode
- Swift
- Math
- String
categories:
- LeetCode
- Swift
- Math
- String
---

# 題目

Given two binary strings, return their sum (also a binary string).

給兩個二元字串，返回他們的加總 (也是一個二元字串)。

---

# 範例

a = "11"
b = "1"
Return "100".

"11" 十進位為 3 ， "1" 十進位為 1 ，相加為 4 ，二進位為 "100"

---

# 解題

將兩個字串轉為字元陣列，定義一個 sum 擺放加總結果，與 carry 判斷是否進位。

從兩個陣列尾端開始做相加，如果加總大於等於 2 ，將加總減去 2 ，且代表需要進位，將 carry 值帶至下一次加總。

每次加總完畢，放入 sum 的第一個位置。

最後結束迴圈時，若還有剩下的 carry 值，放進 sum ，返回 sum 的字串。

``` swift
func addBinary(_ a: String, _ b: String) -> String {
    let a = Array(a)
    let b = Array(b)
    var i = a.count, j = b.count
    var sum = [Character]()
    var carry = 0
    
    while i != 0 || j != 0 {
        var first = 0, second = 0
        if i - 1 >= 0 { first = Int(String(a[i - 1]))! }
        if j - 1 >= 0 { second = Int(String(b[j - 1]))! }
        
        var temp = first + second + carry
        carry = 0
        if temp >= 2 {
            temp -= 2
            carry += 1
        }
        sum.insert(Character(String(temp)), at: 0)
        
        if i != 0 { i -= 1 }
        if j != 0 { j -= 1 }
    }
    if carry == 1 { sum.insert(Character(String(carry)), at: 0) }
    return String(sum)
}
```