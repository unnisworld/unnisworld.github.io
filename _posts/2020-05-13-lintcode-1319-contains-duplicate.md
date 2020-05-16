---
layout: post
title:  "LintCode 878 : Boundary of Binary Tree"
date:   2020-05-10
categories: leetcode-medium leetcode Tree
---

Solution to [Boundary of Binary Tree][leetcode] Problem.


{% highlight java %}
public class Solution {
    
    List<Integer> result = new ArrayList<>();
    
    /**
     * @param root: a TreeNode
     * @return: a list of integer
     */
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        if(root == null)
            return Collections.emptyList();
        // write your code here
        result.add(root.val);
        traverseLeftSide(root.left);
        traverseLeafNodes(root);
        traverseRightSide(root.right);
        
        return result;
    }
    
    private void traverseLeftSide(TreeNode node) {
        if(node == null || isLeafNode(node))
            return;
            
        result.add(node.val);
        
        if(node.left != null) {
            traverseLeftSide(node.left);
        } else {
            traverseLeftSide(node.right);
        }
    }
    
    private void traverseLeafNodes(TreeNode node) {
        if(node == null)
            return;
        if(isLeafNode(node))
            result.add(node.val);
        else {
            traverseLeafNodes(node.left);
            traverseLeafNodes(node.right);
        }    
    }
    
    private void traverseRightSide(TreeNode node) {
        if(node == null || isLeafNode(node))
            return;
        
        if(node.right != null) {
            traverseRightSide(node.right);
        } else {
            traverseRightSide(node.left);
        }
        
        result.add(node.val);
    }
    
    private boolean isLeafNode(TreeNode node) {
        return node.left == null && node.right == null;
    }
}
{% endhighlight %}

[leetcode]: https://www.lintcode.com/problem/boundary-of-binary-tree
