---
layout: post
title:  "Path Sum"
date:   2020-03-04 16:15:00 +0530
categories: leetcode leetcode-simple Tree
---

Solution to [Path Sum][leetcode] problem. I came up with this solution, but was blown away when I saw the  solution by [Lazy Coder][lazy-coder].

{% highlight java %}
class Solution {
    boolean result = false;
    public boolean hasPathSum(TreeNode root, int sum) {
        int curSum = 0;
        preOrderTraverse(root, sum, curSum);
        return result;
    }
    
    private void preOrderTraverse(TreeNode node, int sum, int curSum) {
      if(node == null) 
          return;
      curSum = curSum + node.val;
      
      if (curSum == sum && isLeafNode(node)) {
          result = true;
          return;
      }
        
      preOrderTraverse(node.left, sum, curSum);
      preOrderTraverse(node.right, sum, curSum);  
    }
    
    private boolean isLeafNode(TreeNode node) {
        return node.left == null && node.right == null;
    }
}
{% endhighlight %}

More elegant solution :

{% highlight java %}

class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        
        if (sum == root.val && root.left == null && root.right == null) {
            return true;
        }
     
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/path-sum
[lazy-coder]: https://leetcode.com/lazy_coder_114/
