---
layout: post
title:  "Leetcode : 203 Remove Linked List Elements"
date:   2020-05-01
categories: leetcode-easy leetcode linkedlist
---

Solution to [Remove Linked List Elements][leetcode] Problem. 
The first approach uses a dummy pointer to handle the edge case of removing head node itself.

Approach 1:

{% highlight java %}
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode();
        dummy.val = -1;
        dummy.next = head;
        
        ListNode cur = head;
        ListNode pre = dummy;
        while(cur != null) {
            if(cur.val == val) {
                pre.next = cur.next;
            } else {
                pre = cur;
            }    
            cur = cur.next;
        }
        
        return dummy.next;
    }
}
{% endhighlight %}

Approach 2:

Approach 2 is more cleaner with less variables. Here is a [video][utube] explaining the same.

{% highlight java %}
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        while(head != null && head.val == val) {
            head = head.next;
        }
        
        ListNode cur = head;
        while(cur != null && cur.next != null) {
            if(cur.next.val == val) {
                cur.next = cur.next.next;
            } else {
                cur = cur.next;
            }
        }
        return head;
    } 
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/linked-list-cycle-ii/
[utube]: https://www.youtube.com/watch?v=gfFn-OXxcgU