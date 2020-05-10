---
layout: post
title:  "LeetCode 199 : Binary Tree Right Side View"
date:   2020-05-10
categories: leetcode-medium leetcode Tree
---

Solution to [Binary Tree Right Side View][leetcode] Problem.

Do level order traversal and keep track of the last element processed in a level. Add the last element of each level to the result list.

{% highlight java %}
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        if(root == null) {
            return Collections.emptyList();
        }
        List<Integer> result = new ArrayList<>();
        
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()) {
            int ls = q.size();
            TreeNode pre = null;
            for(int i=0;i<ls;i++) {
                TreeNode cur = q.remove();
                if(cur.left != null)
                    q.add(cur.left);
                if(cur.right != null)
                    q.add(cur.right);
                pre = cur;
            }
            result.add(pre.val);
            
        }
        
        return result;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/binary-tree-right-side-view
