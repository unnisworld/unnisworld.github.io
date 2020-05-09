---
layout: post
title:  "Leetcode 142 : Linked List Cycle ii"
date:   2020-05-01
categories: leetcode-medium leetcode linkedlist
---

Solution to [Return begining node of a Linked List Cycle][leetcode] Problem. 
This [resource][java2s] contains an excellent explanation of why the below approach works.

{% highlight java %}
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode sp = head;
        ListNode fp = head;
        
        boolean hasCycle = false;
        while(fp != null && fp.next != null) {
            fp = fp.next.next;
            sp = sp.next;
            
            if(fp == sp) {
                hasCycle = true;
                break;
            }
        }
        
        if(!hasCycle) {
            return null;
        }
        
        sp = head;
        while(fp != sp) {
            sp = sp.next;
            fp = fp.next;
        }
        
        return sp;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/linked-list-cycle-ii/
[java2s]: https://java2blog.com/find-start-node-of-loop-in-linkedlist/