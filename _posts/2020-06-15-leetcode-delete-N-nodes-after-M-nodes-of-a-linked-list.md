---
layout: post
title:  "Leetcode 1474 : Delete N Nodes After M Nodes of a Linked List"
date:   2020-06-15 21:50:00 +0530
categories: leetcode leetcode-easy LinkedList
---

Solution to [Delete N Nodes After M Nodes of a Linked List][leetcode] problem.

{% highlight java %}
class Solution {
    public ListNode deleteNodes(ListNode head, int m, int n) {
        ListNode pre = null;
        ListNode cur = head;
        
        while(cur != null) {
            int i = m, j = n;
            
            while(cur != null && i > 0) {
                pre = cur;
                cur = cur.next;
                i--;
            }
            
            while(cur != null && j > 0) {
                cur = cur.next;
                j--;
            }
            
            pre.next = cur;
        }
        
        return head;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/
