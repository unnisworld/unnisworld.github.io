---
layout: post
title:  "Reverse Linked List"
date:   2020-02-22 11:36:00 +0530
categories: leetcode leetcode-easy LinkedList
---

Solution to [Reverse Linked List][leetcode] problem.

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
    
    public ListNode reverseList(ListNode head) {
        return reverse(head, null);
    }
    
    private ListNode reverse(ListNode cur, ListNode prev) {
        if (cur == null)
            return prev;
        
        ListNode next = cur.next;
        cur.next = prev;
        
        // Tail Recursion - http://www.lua.org/pil/6.3.html
        // https://stackoverflow.com/questions/33923/what-is-tail-recursion/34540#34540
        return reverse(next, cur);
    }
    
// iterative solution    
//     public ListNode reverseList(ListNode head) {
//         if (head == null || head.next == null)
//             return head;
        
//         ListNode cur = head;
//         ListNode prev = null;
        
//         while(cur != null) {
//             ListNode next = cur.next;
//             cur.next = prev;
//             prev = cur;
//             cur = next;
//         }
        
//         return prev;
//     }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/reverse-linked-list/
