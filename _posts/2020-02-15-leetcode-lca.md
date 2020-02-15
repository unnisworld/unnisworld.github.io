---
layout: post
title:  "Lowest Common Ancestor of a Binary Tree"
date:   2020-02-15 22:20:00 +0530
categories: leetcode leetcode-medium tree lca
---

Solution to [Lowest Common Ancestor of a Binary Tree][leetcode] problem.

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
    
    TreeNode ans;
    
    public TreeNode lowestCommonAncestor(TreeNode currentNode, TreeNode p, TreeNode q) {
        findlca(currentNode, p, q);
        return ans;
    }
    
    private boolean findlca(TreeNode currentNode, TreeNode p, TreeNode q) {
        if(currentNode == null)
            return false;
        
        boolean self = (currentNode == p) || (currentNode == q);
        boolean left = findlca(currentNode.left, p, q);
        boolean right = findlca(currentNode.right, p, q);
        
        if ( (left && right) || (self && right) || (self && left) )
            ans = currentNode;
        
        return self || left || right;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/
