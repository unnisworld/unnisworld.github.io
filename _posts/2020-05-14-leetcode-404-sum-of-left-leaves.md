---
layout: post
title:  "LeetCode 404 : Sum of Left Leaves"
date:   2020-05-14
categories: leetcode-easy leetcode Tree
---

Solution to [Sum of Left Leaves][leetcode] Problem. Here is a [nice video][utube] which explains the approach.

Solution 1

{% highlight java %}
class Solution {
    
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null)
            return 0;
        
        if(root.left != null && isLeafNode(root.left)) {
            return root.left.val + sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
        } else {
            return sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
        }
    }

    private boolean isLeafNode(TreeNode node) {
        return node.left == null && node.right == null;
    }
}
{% endhighlight %}

Solution 2

{% highlight java %}
class Solution {
    
    public int sumOfLeftLeaves(TreeNode root) {
        return findSum(root, null);
    }
    
    private int findSum(TreeNode node, TreeNode parent) {
        if(node == null)
            return 0;
        
        int curSum = 0;
        if(parent != null && parent.left == node && isLeafNode(node))
            curSum = node.val;
        
        return curSum + findSum(node.left, node)
                        + findSum(node.right, node);
    }

    private boolean isLeafNode(TreeNode node) {
        return node.left == null && node.right == null;
    }
}
{% endhighlight %}


[leetcode]: https://leetcode.com/problems/sum-of-left-leaves/
[utube]: https://www.youtube.com/watch?v=_gnyuO2uquA
