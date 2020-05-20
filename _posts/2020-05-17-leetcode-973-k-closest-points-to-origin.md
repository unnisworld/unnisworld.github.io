---
layout: post
title:  "LeetCode 973 : K Closest Points to Origin"
date:   2020-05-17
categories: leetcode-medium leetcode Kth-problem
---

Solution to [K Closest Points to Origin][leetcode] Problem. Check out this [nice description][desc] on different approaches available to solve this problem.

{% highlight java %}
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        PriorityQueue< int[] > pq = new PriorityQueue<>(
    (p1,p2) ->  p2[0] * p2[0] + p2[1] * p2[1] - p1[0] * p1[0] - p1[1] * p1[1]);
        
        for(int[] p : points) {
            pq.offer(p);
            if(pq.size() > K) {
                pq.poll();
            }
        }
        
        int[][] result = new int[K][2]; 
        int i = 0;
        while(pq.size() != 0) {
            result[i++] = pq.poll();
        }
        
        return result;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/k-closest-points-to-origin/
[desc]: https://leetcode.com/problems/k-closest-points-to-origin/discuss/220235/Java-Three-solutions-to-this-classical-K-th-problem.
