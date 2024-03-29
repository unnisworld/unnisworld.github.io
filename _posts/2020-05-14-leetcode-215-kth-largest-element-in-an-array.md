---
layout: post
title:  "LeetCode 215 : Kth Largest Element in an Array"
date:   2020-05-14
categories: leetcode-medium leetcode array Kth-problem
---

Solution to [Kth Largest Element in an Array][leetcode] Problem. Here is a [nice video][utube] which explains the approach.

{% highlight java %}
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        
        for(int i : nums) {
            minHeap.add(i);
            if(minHeap.size() > k) {
                minHeap.remove();
            }
        }
        
        return minHeap.remove();
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/kth-largest-element-in-an-array/
[utube]: https://www.youtube.com/watch?v=FrWq2rznPLQ
