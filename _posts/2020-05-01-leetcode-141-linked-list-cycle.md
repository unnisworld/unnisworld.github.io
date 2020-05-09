---
layout: post
title:  "Leetcode 141 : Linked List Cycle"
date:   2020-05-01
categories: leetcode-easy leetcode linkedlist
---

Solution to [Linked List Cycle][leetcode] Problem.

{% highlight java %}
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode sp = head;
        ListNode fp = head;
        
        while(fp != null && fp.next != null) {
            fp = fp.next.next;
            sp = sp.next;
            
            if(fp == sp)
                return true;
        }
        
        return false;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/linked-list-cycle/
