---
layout: post
title: "LeetCode 1004 · Max Consecutive Ones III"
date: 2021-10-16
categories: lintcode lintcode-medium SlidingWindow
---

Solution to [Max Consecutive Ones III][leetcode] problem. See this [Youtube video][video] for the explanation.

{% highlight java %}
class Solution {
    public int longestOnes(int[] nums, int k) {
        int n = nums.length;
        if (n <= k) return n;
        
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
            while(flipCount > k) {
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

[leetcode]: https://leetcode.com/problems/max-consecutive-ones-iii/
[video]: https://www.youtube.com/watch?v=ROuOZongV6I
