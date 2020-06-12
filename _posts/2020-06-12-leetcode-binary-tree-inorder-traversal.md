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
        List<Integer> result = new ArrayList<>();
        LinkedList<TreeNode> s = new LinkedList<>();
        
        TreeNode cur = root;
        while(!s.isEmpty() || cur != null) {
            while(cur != null) {
                s.push(cur);
                cur = cur.left;
            }
            
            cur = s.pop();
            result.add(cur.val);
            cur = cur.right;
        }
        
        return result;
    }

}    
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/binary-tree-inorder-traversal/
