---
layout: post
title:  "Leetcode 53 : Maximum Subarray"
date:   2020-04-18
categories: leetcode leetcode-easy subarray
---

Solution to [Maximum Subarray][leetcode] problem. [Checkout] this [resource] to understand how this approach work. 


{% highlight java %}
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        
        int curMax = nums[i];
        int allMax = nums[i];
        for(int i=1;i<nums.length;i++) {
            curMax = Math.max(nums[i], curMax + nums[i]);
            allMax = Math.max(curMax, allMax);
        }

        return allmax;    
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/maximum-subarray/
[resource]:https://medium.com/@rsinghal757/kadanes-algorithm-dynamic-programming-how-and-why-does-it-work-3fd8849ed73d
