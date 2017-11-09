---
title: LeetCode#112 Path Sum - in Swift
date: 2017-11-01 13:49:12
tags:
- LeetCode
- Swift
- Tree
- Depth-first Search
categories:
- LeetCode
- Swift
- Tree
- Depth-first Search
---

# 題目

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

給一二元樹和目標值，找出樹中是否有「根到葉」的路徑，路徑上所有節點的加總等於目標值。

---

# 範例

``` swift
Given the below binary tree and sum = 22,

        5
       / \
      4   8
     /   / \
    11  13  4
   /  \      \
  7    2      1

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
```

給上方二元樹，以及目標值 22 。

返回 true ， 因為有一條「根到葉」路徑 5 -> 4 -> 11 -> 2 其加總為 22 。

---

# 解題

從根開始堆疊節點總和，一旦到達葉節點且堆疊的總和等於目標值，即可返回答案。

``` swift
func hasPathSum(_ root: TreeNode?, _ sum: Int) -> Bool {
    if root == nil { return false }
    
    func findSum(_ root: TreeNode?, _ heap: Int) -> Bool {
        guard let root = root else { return false }
        var heap = heap
        heap += root.val
        if root.left == nil && root.right == nil && heap == sum { return true }
        return findSum(root.left, heap) || findSum(root.right, heap)
    }
    
    return findSum(root, 0)
}
```