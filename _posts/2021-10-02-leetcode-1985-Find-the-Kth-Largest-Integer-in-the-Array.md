---
layout: post
title: "Leetcode 1985. Find the Kth Largest Integer in the Array"
date: 2021-10-02
categories: leetcode leetcode-medium Heap
---

Solution to [Find the Kth Largest Integer in the Array][leetcode] problem.

In Java we need to use custom comparator since the default comparator is string comparator which compares by lexicographical order. It means for example: default comparator will treat "123" < "14" because "2" < "4". So to overcome this, we will have a comparator which uses compareTo() method only if the string length of two objects to be compared is same, otherwise we will use the string.length() to identify which string/number is larger.

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

[Here is a good article][priorityqueue] to refresh your understanding about Priority Queues in Java.

Complexity

Time: O(NlogK * M), where N <= 10^4 is length of nums array, K <= N is the kth largest element need to output, M <= 100 is length of each num.
Explanation: The MinHeap keeps up to K elements, each heappush/heappop operator costs O(logK). We iterate all elements in nums and push/pop to the MinHeap N times. We need to multiply by M as well, since in the worst case, we need to compare strings lexicographically.
Space: O(K)

[leetcode]: https://leetcode.com/problems/find-the-kth-largest-integer-in-the-array/
[priorityqueue]:https://www.scaler.com/topics/java-priority-queue-comparator/
