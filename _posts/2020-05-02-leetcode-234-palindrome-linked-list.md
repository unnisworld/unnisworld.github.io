---
layout: post
title:  "Leetcode 234 : Palindrome Linked List"
date:   2020-05-02
categories: leetcode-easy leetcode linkedlist
---

Solution to [Palindrome Linked List][leetcode] Problem. Watch this [video][utube] for more detailed explanation.

{% highlight java %}
class Solution {
    
    public boolean isPalindrome(ListNode head) {
        ListNode fp = head;
        ListNode sp = head;
        while(fp != null && fp.next != null) {
            fp = fp.next.next;
            sp = sp.next;
        }
        
        // Now sp will be at the middle of the list
        ListNode middlePtr = reverse(sp, null);
        
        ListNode startPtr = head;
        while(middlePtr != null) {
            if(middlePtr.val != startPtr.val)
                return false;
            
            startPtr = startPtr.next;
            middlePtr = middlePtr.next;
        }
        
        return true;
    }
    
    private ListNode reverse(ListNode cur, ListNode pre) {
        if(cur == null)
            return pre;
        
        ListNode nxt = cur.next;
        cur.next = pre;
        return reverse(nxt, cur);
    }
} 
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/palindrome-linked-list/
[utube]: https://www.youtube.com/watch?v=wk4QsvwQwdQ