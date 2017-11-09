---
title: LeetCode#111 Minimum Depth of Binary Tree - in Swift
date: 2017-11-07 14:18:53
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

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

給定二元樹，找出最小深度。

最小深度代表由根節點至某個最近的葉節點所畫出的最短路徑。

---

# 範例

``` swift
Input:
        1
       / \
      2   3
     / \
    4   5

Output: 2
```
有一條最短路徑為 1 -> 3 ，其深度為 2 。

---

# 解題

對樹進行 dps ，並且每下一層就將 depth 值 + 1 ，直到走到葉節點時，

比對這條路徑的深度跟答案的最小值，即可求出最終答案。

``` swift
func minDepth(_ root: TreeNode?) -> Int {
    if root == nil { return 0 }
    var res = Int.max
    func dig(_ root: TreeNode?, _ depth: Int) {
        guard let root = root else { return }
        var depth = depth
        depth += 1
        if root.left == nil && root.right == nil {
            res = min(depth, res)
        }
        dig(root.left, depth)
        dig(root.right, depth)
    }
    
    dig(root, 0)
    return res
}
```