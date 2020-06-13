---
layout: post
title:  "Lowest Common Ancestor of a Binary Search Tree"
date:   2020-02-15 22:20:00 +0530
categories: leetcode leetcode-medium Tree LCA
---

Solution to [Lowest Common Ancestor of a Binary Search Tree][leetcode] problem.

{% highlight java %}
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null)
            return root;
        
        int rootVal = root.val, pVal = p.val, qVal = q.val;
        
        if (pVal > rootVal && qVal > rootVal) 
            return lowestCommonAncestor(root.right, p, q);
        
        if (pVal < rootVal && qVal < rootVal) 
            return lowestCommonAncestor(root.left, p, q);
        
        return root;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/
