---
layout: post
title:  "Sort List"
date:   2020-06-10 20:36:00 +0530
categories: leetcode leetcode-medium LinkedList Sort MergeSort
---

Solution to [Sort List][leetcode] problem. See this [video][vdo] for explanation.

{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode sortList(ListNode head) {
        if(head == null || head.next == null)
            return head;
        
        ListNode temp = null;
        ListNode slow = head, fast = head;
        while(fast != null && fast.next != null) {
            temp = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        temp.next = null;
        
        ListNode firstListHead = sortList(head);
        ListNode secondListHead = sortList(slow);
        
        return merge(firstListHead, secondListHead);
    }
    
    private ListNode merge(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode();
        ListNode pre = dummy;
        while(l1 != null && l2 != null) {
            if(l1.val <= l2.val) {
                pre.next = l1;
                l1 = l1.next;
            } else {
                pre.next = l2;
                l2 = l2.next;    
            }
            pre = pre.next;
        }
        
        pre.next = l1==null ? l2 : l1;
        
        return dummy.next;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/sort-list/
[vdo]: https://www.youtube.com/watch?v=pNTc1bM1z-4
