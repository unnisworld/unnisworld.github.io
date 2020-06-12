---
layout: post
title:  "Leetcode 144 : Binary Tree Preorder Traversal"
date:   2020-06-12 18:20:00 +0530
categories: leetcode leetcode-medium Tree DFS Preorder
---

Solution to [Binary Tree Preorder Traversal][leetcode] problem.

{% highlight java %}
class Solution {
    
 public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();

        TreeNode cur = root;
        while(!stack.isEmpty() || cur != null){
            while(cur != null){
                result.add(cur.val);
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            cur = cur.right;
        }
        return result;
    }
}    
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/binary-tree-preorder-traversal/
