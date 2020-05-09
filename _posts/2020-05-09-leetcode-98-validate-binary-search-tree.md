---
layout: post
title:  "Leetcode 98 : Validate Binary Search Tree"
date:   2020-05-09
categories: leetcode-medium leetcode BST
---

Solution to [Validate Binary Search Tree][leetcode] Problem.

{% highlight java %}
class Solution {
    public boolean isValidBST(TreeNode root) {        
        return isValidBST(root, null, null);      
    }
    
    private boolean isValidBST(TreeNode node, TreeNode min, TreeNode max) {
        if(node == null)
            return true;
        
        if(min != null && node.val <= min.val || max != null && node.val >= max.val) {
            return false;
        }
        
        return isValidBST(node.left, min, node) && isValidBST(node.right, node, max);
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/validate-binary-search-tree/