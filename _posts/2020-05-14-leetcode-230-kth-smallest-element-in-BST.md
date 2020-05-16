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
        return iterateInOrderAndFetchKthElement(root, k);
    }
    
    private int iterateInOrderAndFetchKthElement(TreeNode root, int k) {
        TreeNode cur = root;
        LinkedList<TreeNode> stack = new LinkedList<>();
        while(cur != null || !stack.isEmpty()) {
            while(cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            
            cur = stack.pop();
            if(--k == 0)
                return cur.val;
            
            cur = cur.right;
        }
        
        return -1;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/kth-smallest-element-in-a-bst/
[lc-article]: https://leetcode.com/articles/kth-smallest-element-in-a-bst/
[gfg-link]: https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/
