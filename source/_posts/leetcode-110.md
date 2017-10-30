---
title: LeetCode#110 Balanced Binary Tree - in Swift
date: 2017-10-21 15:16:23
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
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

給一二元樹，驗證它是否高度平衡。

高度平衡的定義為，二元樹其兩個子樹的每個節點的深度不超過 1 。

---

# 範例
Example 1:
``` swift
Input:
       5
      / \
     3   4
    / \   \
   2   6   1

Output: True
```
該二元樹其兩個子樹的每個節點，深度差皆不超過 1 ，為高度平衡。


Example 2:
``` swift
Input:
       5
      / \
     3   4
    / \   \
   2   6   1
          /
         7

Output: False
```
該二元樹倒節點 4 時，其左子樹為空，深度為 1，右子樹持續走到 7 ，深度為 3 ， 3 - 1 > 1 ，不為高度平衡。

---

# 解題

要確定每一個節點的左右子樹是否高度平衡，利用 findDepth 找出該節點的深度，再比較左右節點的差是否大於 1 。

再來要確定每一個節點的平衡，利用遞迴對整棵樹的每一個節點進行一次上述的比較。

``` swift
func isBalanced(_ root: TreeNode?) -> Bool {
    
    func findDepth(_ root: TreeNode?) -> Int{
        if root == nil { return 0 }
        return max(findDepth(root!.left), findDepth(root!.right)) + 1
    }
    
    if root == nil { return true }
    let left = findDepth(root!.left)
    let right = findDepth(root!.right)
    
    return abs(left - right) <= 1 && isBalanced(root!.left) && isBalanced(root!.right)
}
```