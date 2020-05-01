---
layout: post
title:  "Leetcode : 160 Intersection of Two Linked Lists"
date:   2020-05-01
categories: leetcode-easy leetcode linkedlist
---

Solution to [Intersection of Two Linked Lists][leetcode] Problem.

Steps :
1. Find length of both the ll's.
2. Find the diff and move the pointer on largest ll by diff steps.
3. Now traverse both the ll's and compare address of nodes to find intersection point. 

{% highlight java %}
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int lenA = findLen(headA);
        int lenB = findLen(headB);
        
        if(lenA > lenB) {
            int diff = lenA - lenB;
            while(diff > 0) {
                headA = headA.next;
                diff--;
            }
        } else {
            int diff = lenB - lenA;
            while(diff > 0) {
                headB = headB.next;
                diff--;
            }
        }
        
        while(headA != null && headB != null) {
            if(headA == headB)
                return headA;
            headA = headA.next; headB = headB.next;
        }
        
        return null;
    }
    
    private int findLen(ListNode head) {
        if(head == null) return 0;
        return 1 + findLen(head.next);
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/intersection-of-two-linked-lists/