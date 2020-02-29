---
layout: post
title:  "Remove Duplicates from Sorted List II"
date:   2020-02-22 08:00:00 +0530
categories: leetcode leetcode-medium LinkedList
---

Solution to [Remove Duplicates from Sorted List II][leetcode] problem.

{% highlight java %}
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null)
            return head;

        // This check is required to safely introduce a dummyHead with value set to MAX_VALUE
        // In a sorted list, if first value is max value, everything else is max value.
        if (head.val == Integer.MAX_VALUE)
            return null;

        // Introduce a dummy node to handle scenarios where even the head node can be duplicate node.
        ListNode dummyHead = new ListNode(Integer.MAX_VALUE);
        dummyHead.next = head;

        ListNode crnt = dummyHead.next;
        ListNode prev = dummyHead;
        while(crnt != null && crnt.next != null) {
            if(crnt.val == crnt.next.val) {
                int dupVal = crnt.val;

                // Skip all the duplicate values.
                do {
                    crnt = crnt.next;
                } while(crnt != null && crnt.val == dupVal);

                prev.next = crnt;
            } else {
                prev = crnt;
                crnt = crnt.next;
            }
        }

        head = dummyHead.next;

        return head;
    }
    

}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/
