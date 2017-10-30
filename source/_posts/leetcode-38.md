---
title: LeetCode#38 Count and Say - in Swift
date: 2017-10-30 13:46:46
tags:
- LeetCode
- Swift
- String
categories:
- LeetCode
- Swift
- String
---

# 題目
The count-and-say sequence is the sequence of integers with the first five terms as following:

``` swift
1.     1
2.     11
3.     21
4.     1211
5.     111221

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
```

Given an integer n, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

"數和說"序列的前五種規則如下所示 :

``` swift
1.     1
2.     11
3.     21
4.     1211
5.     111221

1 是 1 ， 因為 1 個 1 所以下一個
2 是 11 ， 因為 2 個 1 所以下一個
3 是 21 ， 因為 1 個 2 ， 1 個 1 ，所以下一個
4 是 1211
```

按照這個順序下去，算出第 n 個的時候 ，他的"數和說"會是多少。

---

# 範例
Example 1:
``` swift
Input: 1
Output: "1"
```

Example 2:
``` swift
Input: 4
Output: "1211"
```
返回的值為字串。

---

# 解題

這題用堆疊的方式做上去， 1 為 "1"

下一個 2 就是 1 的 count and say ，所以 `1` 個 `1` 等於 "11"

下一個 3 就是 2 的 count and say ，所以 "11" 為 `2` 個 `1` 等於 "21"

下一個 4 就是 3 的 count and say ，所以 "21" 為 `1` 個 `2` 和 `1` 個 `1` 等於 "1211"

下一個 5 就是 4 的 count and say ，所以 "1211" 為 `1` 個 `1` 和 `1` 個 `2` 和 `2` 個 `1` 等於 "111221"

``` swift
func countAndSay(_ n: Int) -> String {
    var res = "1"
    if n <= 1 { return res }
    for _ in 2...n {
        res = convertNext(res)
    }
    return res
}
```

那要怎麼算出 count and say ，我們設計一個函式來計算。

例如 5 要求 4 ("1211") 的 count and say ，只要走過字串，定義當下的值以及累加的次數，遇到不同值就寫進新的字串中，並且更新當下值以及累加次數。

別忘了還要再把最後沒加進新字串的值加進去。

``` swift
1 -> temp = "1" , count = 1, new = ""
2 -> temp = "2" , count = 1, new = "11"
1 -> temp = "1" , count = 1, new = "1112"
1 -> temp = "1" , count = 2, new = "1112"
end
new = "111221"
```

``` swift
func convertNext(_ last: String) -> String {
    let arr = Array(last.characters)
    var count = 0
    var temp = ""
    var new = ""
    var i = 0
    while i != arr.count {
        
        if temp != String(arr[i]) {
            new += count == 0 ? "" : String(count) + temp
            temp = String(arr[i])
            count = 1
        } else {
            count += 1
        }
        i += 1
    }
    
    new += String(count) + temp
    return new
}
```