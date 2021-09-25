---
layout: post
title: "Leetcode 328 : Odd Even Linked List"
date: 2021-09-25
categories: leetcode leetcode-medium LinkedList
---

Solution to [Odd Even Linked List][leetcode] problem.

{% highlight java %}
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if(head == null)
            return head;
        
        ListNode oddHead = head;
        ListNode evenHead = head.next;
        
        ListNode curOdd = head;
        ListNode curEven = evenHead;
        while(curEven != null && curEven.next != null) {
            curOdd.next = curEven.next;
            curOdd = curOdd.next;
            curEven.next = curOdd.next;
            curEven = curEven.next;
        }
        
        curOdd.next = evenHead;
        
        return head;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/odd-even-linked-list/
