---
layout: post
title:  "LintCode 1094 : Car Pooling"
date:   2020-05-20
categories: leetcode-medium Interval-Problems
---

Solution to [Car Pooling][leetcode] Problem.


{% highlight java %}
class Solution {
    public boolean carPooling(int[][] trips, int capacity) {
        int[][] tripsSortedBasedOnEndingTime = trips.clone();
        Arrays.sort(trips, (a,b) -> a[1] - b[1]);
        Arrays.sort(tripsSortedBasedOnEndingTime, (a,b) -> a[2] - b[2]);
        
        int j = 0;
        for(int[] i : trips) {
            while (tripsSortedBasedOnEndingTime[j][2] <= i[1]) {
                capacity += tripsSortedBasedOnEndingTime[j][0];
                j++;
            }
            
            if (capacity < i[0]) {
                return false;
            }
            
            capacity -= i[0];
        }
        
        return true;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/car-pooling
