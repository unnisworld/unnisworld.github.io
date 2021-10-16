---
layout: post
title: "LintCode 883 · Max Consecutive Ones II"
date: 2021-10-16
categories: lintcode lintcode-medium SlidingWindow
---

Solution to [Max Consecutive Ones II][lintcode] problem.

{% highlight java %}
public class Solution {
    /**
     * @param nums: a list of integer
     * @return: return a integer, denote  the maximum number of consecutive 1s
     */
    public int findMaxConsecutiveOnes(int[] nums) {
        int n = nums.length;
        if (n < 2) return n;

        // Sliding window pointers
        int L = 0, R = 0;
    
        // Track flip count and max length
        int flipCount = 0, maxLen = 0;
        
        // Slide over the array elements
        while(R < n) {
            if (nums[R] == 0) {
                flipCount++;
            }

            // contract window if we don't meet the condition
            while(flipCount > 1) {
                if (nums[L] == 0) {
                    flipCount--;
                }
                L++;
            }

            // update maxlen
            maxLen = Math.max(maxLen, R - L + 1);
            
            R++;
        }

        return maxLen;
    }
}
{% endhighlight %}

[lintcode]: https://www.lintcode.com/problem/883/description
