---
layout: post
title:  "Search in Rotated Sorted Array"
date:   2020-02-02 8:30:00 +0530
categories: leetcode-medium leetcode binarysearch
---

Solution to [Find First and Last Position of Element in Sorted Array][leetcode].

While going through the code, have a look at the diagram in [this link][theoryofprogramming] to get a grasp on how we are picking the right partition during each iteration.  

{% highlight java %}
class Solution {
    public int search(int[] nums, int target) {
        if (nums.length < 1) return -1;
        int s = 0;
        int e = nums.length - 1;
        int m;

        while (s <= e) {
            m = (s + e) / 2;
            if (target == nums[m]) return m;

            if (nums[s] <= nums[m]) { /* Array is sorted from s to m */
                if (nums[m] > target && nums[s] <= target) // check if target is in sorted part
                    e = m - 1;
                else s = m + 1;
            } else { // Array is sorted from m to e
                if (nums[m] < target && nums[e] >= target) // check if target is in sorted part
                    s = m + 1;
                else e = m - 1;
            }
        }
        return -1;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/search-in-rotated-sorted-array/
