---
layout: post
title: "Leetcode 1985. Find the Kth Largest Integer in the Array"
date: 2021-10-02
categories: leetcode leetcode-medium Heap
---

Solution to [Find the Kth Largest Integer in the Array][leetcode] problem.

{% highlight java %}
class Solution {
    public String kthLargestNumber(String[] nums, int k) {
        PriorityQueue<String> minHeap = new PriorityQueue<>((o1, o2) -> {
            if (o1.length() == o2.length()) {
                return o1.compareTo(o2);
            }
            
            return Integer.compare(o1.length(), o2.length());
        });
        
        for (String s : nums) {
            minHeap.add(s);
            
            if (minHeap.size() > k) {
                minHeap.remove();
            }
        }
        
        return minHeap.remove();
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-the-kth-largest-integer-in-the-array/
