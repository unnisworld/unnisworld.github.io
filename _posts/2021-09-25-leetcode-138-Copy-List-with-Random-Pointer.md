---
layout: post
title: "Leetcode 138 : Copy List with Random Pointer"
date: 2021-09-25
categories: leetcode leetcode-medium LinkedList
---

Solution to [Copy List with Random Pointer][leetcode] problem.

See [this video][youtube] for nice explanation of the solution. 

{% highlight java %}
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null)
            return head;
        
        Node cur = head;
        
        // Step 1: Create clone nodes A->A`->B->B`
        while(cur != null) {
            Node curClone = new Node(cur.val);
            curClone.next = cur.next;
            cur.next = curClone;
            
            cur = curClone.next;
        }
        
        // Step 2: Connect random nodes
        cur = head;
        while(cur != null) {
            if (cur.random != null) {
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }
        
        // Step 3: Detach cloned nodes
        Node cloneHead = head.next;
        
        cur = head;
        Node curClone = head.next;
        while(cur != null) {
            cur.next = curClone.next;
            if(cur.next != null) {
                curClone.next = cur.next.next;
            }
            cur = cur.next;
            curClone = curClone.next;
        }
        
        return cloneHead;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/copy-list-with-random-pointer/
[youtube]: https://www.youtube.com/watch?v=xbpUHSKoALg
