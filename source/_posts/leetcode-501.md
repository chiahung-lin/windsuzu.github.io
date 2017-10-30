---
title: LeetCode#501 Find Mode in Binary Search Tree - in Swift
date: 2017-10-23 16:14:51
tags:
- LeetCode
- Swift
- Tree
categories:
- LeetCode
- Swift
- Tree
---

# 題目
Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.

給一二元搜尋樹 (BST) 包含重複節點，找出該樹的眾數 (mode(s)) (可能有多個) (出現最多次的元素) 。

Assume a BST is defined as follows:

1. The left subtree of a node contains only nodes with keys less than or equal to the node's key.
2. The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
3. Both the left and right subtrees must also be binary search trees.

假設該 BST 定義為下:

1. 左子樹只包含「小於或等於」的節點
2. 右子樹只包含「大於或等於」的節點
3. 其餘左右子樹必須維持上述的規則

# 範例

For example:
``` swift
Given BST [1,null,2,2],
   1
    \
     2
    /
   2

return [2].
```

Note: If a tree has more than one mode, you can return them in any order.

如果不止一個眾數，請回傳一個沒有限制排序的陣列。

---

# 解題

這個做法不為最佳解，也不限制只能在 BST ，可以使用在任何二元樹。

利用 map 記錄每一個節點值出現的次數，並且不斷更新 maxVal (最多出現次數)的值。

走完一遍樹後，再從 map 中找出所有 v (次數) 等於 maxVal 的節點 k ，加進 result 中。

``` swift
func findMode(_ root: TreeNode?) -> [Int] {
    if root == nil { return [] }
    
    var dict = [Int:Int]()
    var maxVal = 0
    
    func traverse(_ root: TreeNode?) {
        if root == nil { return }
        
        dict[root!.val] = dict[root!.val] != nil ? dict[root!.val]! + 1 : 1
        maxVal = max(dict[root!.val]!, maxVal)
        
        traverse(root!.left)
        traverse(root!.right)
    }
    
    traverse(root)
    
    var res = [Int]()
    for (k,v) in dict {
        if v == maxVal { res.append(k) }
    }
    
    return res
}
```
