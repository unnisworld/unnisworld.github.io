---
layout: post
title:  "LeetCode 513 : Find Bottom Left Tree Value"
date:   2020-05-10
categories: leetcode-medium leetcode Tree
---

Solution to [Find Bottom Left Tree Value][leetcode] Problem.

Do level order traversal and keep track of left most node when we start processing a level.
Return the final value of leftmostNode.

{% highlight java %}
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        
        TreeNode leftmostNode = root;
        while(!q.isEmpty()) {
            int ls = q.size();
            for(int i=0;i<ls;i++) {
                TreeNode node = q.remove();
                if(i==0) {
                   leftmostNode = node;
                }
                if(node.left != null)
                    q.add(node.left);
                if(node.right != null)
                    q.add(node.right);
            }
        }
        
        return leftmostNode.val;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-bottom-left-tree-value/
