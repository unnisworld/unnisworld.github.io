---
layout: post
title:  "Leetcode 978 : Longest Turbulent Subarray"
date:   2020-04-29
categories: leetcode leetcode-medium subarray array
---

Solution to [Longest Turbulent Subarray][leetcode] problem.

{% highlight java %}
class Solution {
    public int maxTurbulenceSize(int[] A) {
        if (A.length == 1) {
            return 1; 
        } else if (A.length == 2) {
            return (A[0] == A[1]) ? 1 : 2;
        }

        int prev = A[0] - A[1];
        int localMax = (prev == 0) ? 1 : 2;
        int globalMax = localMax;  

        for (int i = 2; i < A.length; i++) {
            int cur = A[i-1] - A[i];

            if ((prev > 0 && cur < 0) || (prev < 0 && cur > 0)) {
                localMax++;
            } else {
                /*--
                 # case analysis
                 prev > 0  && cur > 0    -> localMax = 2   a > b > c
                 prev < 0  && cur < 0    -> localMax = 2   a < b < c 
                 prev == 0 && cur != 0   -> localMax = 2   a = a ? b
                 prev !=0  && cur == 0   -> localMax = 1   a ? b = b
                 prev == 0 && cur == 0   -> localMax = 1   a = a = a 
                ---*/
                localMax = (cur == 0) ? 1 : 2;
            }

            globalMax = Math.max(globalMax, localMax);
            prev = cur;
        }

        return globalMax;
    }
}    
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/longest-turbulent-subarray/
