---
layout: post
title:  "Non-decreasing Array"
date:   2020-02-09 11:30:00 +0530
categories: leetcode-easy leetcode array
---

Solution to ["Non-decreasing Array" problem][leetcode]. 

{% highlight java %}
class Solution {
    public boolean checkPossibility(int[] nums) {
        int max = Integer.MIN_VALUE;
        int c = 0;
        for (int i = 0; i < nums.length; i ++) {
            if (max <= nums[i]) {
                max = nums[i];
            } else {
                c ++;
            }
        }
        int min = Integer.MAX_VALUE;
        int d = 0;
        for (int i = nums.length - 1; i >= 0; i --) {
            if (min >= nums[i]) {
                min = nums[i];
            } else {
                d ++;
            }
        }
        return ((c <= 1 || d <= 1) ? true : false);
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/non-decreasing-array/
