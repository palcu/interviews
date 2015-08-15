---
title:  "Check if a tree is balanced"
date:   2015-08-15 15:50:00
description: "Neat trick for a shorter code"
---

> Given a binary tree, determine if it is height-balanced.
> For this problem, a height-balanced binary tree is defined as a binary tree in
> which the depth of the two subtrees of every node never differ by more than 1.

[_LeetCode_](https://leetcode.com/problems/balanced-binary-tree/)

In the O(N^2) solution you naively traverse the left and right subtrees for
every node in the tree. But this can be improved, because you could return the
depth and the say that the tree from that nodeit is balanced in the same 
function. However, I've struggled with the fact that I should have returned a
pair of a boolean (is the tree balanced) and int (the height of the tree). The
trick in Cracking the Coding Interview is to return `-1` if the tree is
unbalanced, and from that the code simplifies a lot.

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
private:
    int checkDepth(TreeNode *node) {
        if (node == nullptr) return 0;
        int left = checkDepth(node->left),
            right = checkDepth(node->right);
        if (left < 0 || right < 0) return -1;
        int diff = abs(left - right);
        if (diff > 1) return -1;
        return 1 + max(left, right);
    }

public:
    bool isBalanced(TreeNode * root) {
        if (root == nullptr)
            return true;
        return checkDepth(root) > 0;
    }
}
```
