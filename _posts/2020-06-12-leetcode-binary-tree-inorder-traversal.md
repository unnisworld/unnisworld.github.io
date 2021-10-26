---
layout: post
title:  "Leetcode 94 : Binary Tree Inorder Traversal"
date:   2020-06-12 18:20:00 +0530
categories: leetcode leetcode-medium Tree DFS Inorder
---

Solution to [Binary Tree Inorder Traversal][leetcode] problem.

{% highlight java %}
class Solution {
    
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        
        recursiveInorder(root, result);
        
        return result;
    }    
    
    private void  recursiveInorder(TreeNode node, List<Integer> result) {
        if(node == null)
            return;
        
        recursiveInorder(node.left, result);
        result.add(node.val);
        recursiveInorder(node.right, result);
    }
}    
{% endhighlight %}

Iterative Solution

{% highlight java %}
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while(cur != null || !stack.isEmpty()) {
            traverseToTheLeftEnd(cur, stack);
            
            cur = stack.pop();
            result.add(cur.val);
            
            cur = cur.right;
        }
        
        return result;
    }
    
    private void traverseToTheLeftEnd(TreeNode cur, Stack stack) {
        while(cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
    }
}   
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/binary-tree-inorder-traversal/
