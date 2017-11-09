---
title: LeetCode#26 Remove Duplicates from Sorted Array - in Swift
date: 2017-10-31 11:26:23
tags:
- LeetCode
- Swift
- Array
- Two Pointers
categories:
- LeetCode
- Swift
- Array
- Two Pointers
---

# 題目
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

給一個已排序陣列，移除那些重複的元素，讓每個元素只出現一次，並且返回移除後陣列的新長度。

不使用額外空間。

---

# 範例
For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

[1,1,2] 應該要返回 2 ，因為 1 重複了兩次。移除後應為 [1,2] 長度為 2 。

---

# 解題

題目雖然只寫到要求回傳新陣列的長度，實際上還會確認是否有正確移除重複的元素。

所以首先定義一個數字可以代表新陣列長度以及當前索引值 (count)，

走遍第一個元素之後，只要當前的元素與前一個元素不同，就將當前元素塞進 count 的索引，並且將 count + 1 。

最後就可以從第二個元素開始堆出不會重複的陣列。

``` swift
func removeDuplicates(_ nums: inout [Int]) -> Int {
    if nums.count < 2 { return nums.count }
    var count = 1
    
    for i in 1..<nums.count {
        if nums[i - 1] != nums[i] {
            nums[count] = nums[i]
            count += 1
        }
    }
    return count
}
```