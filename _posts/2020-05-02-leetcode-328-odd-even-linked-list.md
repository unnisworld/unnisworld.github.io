---
layout: post
title:  "Leetcode : 328 Odd Even Linked List"
date:   2020-05-01
categories: leetcode-medium leetcode linkedlist
---

Solution to [Odd Even Linked List][leetcode] Problem. Watch this [video][utube] for more detailed explanation.

{% highlight java %}
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if(head == null)
            return head;
        
        ListNode oddStart = head;
        ListNode evenStart = head.next;

        ListNode evenCur = evenStart;
        ListNode oddCur = oddStart;
        while(oddCur != null && oddCur.next != null && evenCur != null && evenCur.next != null) {
            // This approach also works
            // oddCur.next  = oddCur.next.next;
            // evenCur.next = evenCur.next.next;
            // oddCur = oddCur.next;
            // evenCur = evenCur.next;
            
            oddCur.next = evenCur.next;
            oddCur = oddCur.next;
            evenCur.next = oddCur.next;
            evenCur = evenCur.next;
        }
        
        oddCur.next = evenStart;
        
        return head;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/odd-even-linked-list/
[utube]: https://www.youtube.com/watch?v=C_LA6SOwVTM