---
layout: post
title:  "LeetCode 111 : Minimum Depth of Binary Tree"
date:   2020-05-10
categories: leetcode-easy leetcode Tree
---

Solution to [Minimum Depth of Binary Tree][leetcode] Problem.

Do level order traversal and stop when you hit the first leef node.

{% highlight java %}
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null)
            return 0;
        
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        
        int depth = 0;
        while(!q.isEmpty()) {
            int ls = q.size();
            depth++;
            for(int i=0;i<ls;i++) {
                TreeNode n = q.remove();
                if(n.left == null && n.right == null)
                    return depth;
                
                if(n.left != null) {
                    q.add(n.left);
                }
                if(n.right != null) {
                    q.add(n.right);
                }
            }
        }
        
        return depth;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/minimum-depth-of-binary-tree/
