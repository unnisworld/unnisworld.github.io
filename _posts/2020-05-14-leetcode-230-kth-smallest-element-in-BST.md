---
layout: post
title:  "LeetCode 230 : Kth Smallest Element in BST"
date:   2020-05-14
categories: leetcode-medium leetcode BST Tree
---

Solution to [Kth Smallest Element in BST][leetcode] Problem. This [leetcode solution article][lc-article] provides a nice intro to different Tree traversal algorithms. This [GFG link][gfg-link] is also useful to understand how to do inorder traversal iteratively.


{% highlight java %}
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        // Steps :
        // Do inorder traversal of BST
        // Inorder traversal will process BST in ascending order
        // Keep a track of the element count by decrementing k
        // when k reaches 0, return the node val at that point
        
        TreeNode cur = root;
        Stack<TreeNode> s = new Stack<>();
        while(cur != null || !s.isEmpty()) {
            // process the left subtree
            while(cur != null) {
                s.push(cur);
                cur = cur.left;
            }
            
            // process the middle element
            cur = s.pop();
            if(--k == 0)
                return cur.val;
            
            // process the right subtree tree
            cur = cur.right;
        }
        
        return - 1;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/kth-smallest-element-in-a-bst/
[lc-article]: https://leetcode.com/articles/kth-smallest-element-in-a-bst/
[gfg-link]: https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/
