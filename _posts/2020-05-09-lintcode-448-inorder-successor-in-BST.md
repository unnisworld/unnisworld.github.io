---
layout: post
title:  "LintCode 448 : Inorder Successor in BST"
date:   2020-05-09
categories: leetcode-medium leetcode BST
---

Solution to [Inorder Successor in BST][leetcode] Problem. Watch this [video][utube] for explanation.

{% highlight java %}
class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(root==null)
            return null;
     
        TreeNode parent = null;
        TreeNode current = root;
        while(current!=null && current.val!=p.val){
            if(current.val > p.val){
                parent = current;
                current = current.left;
            }else{
                current = current.right;
            }
        }
     
        if(current==null)        
            return null;
     
        if(current.right==null)
            return parent;
     
        current = current.right;
        while(current.left!=null)
            current = current.left;
     
        return current;
    }
}
{% endhighlight %}

[leetcode]: https://www.lintcode.com/problem/inorder-successor-in-bst/description
[utube]: https://www.youtube.com/watch?v=5cPbNCrdotA&vl=en
