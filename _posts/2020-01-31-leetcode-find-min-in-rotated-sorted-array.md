---
layout: post
title:  "Find Minimum in rotated sorted array"
date:   2020-01-29 5:30:00 +0530
categories: leetcode-medium leetcode binarysearch
---

Solution to [Find Minimum in Rotated Sorted Array][leetcode].

{% highlight java %}
class Solution {
    public int findMin(int[] nums) {
        int low=0, high=nums.length-1;
        
        if (nums.length == 1)
            return nums[0];
        
        if (nums.length == 2)
            return nums[0] < nums[1] ? nums[0] : nums[1];
        
        // handle [1,2,3,4,5] kind of inputs
        if (nums[low] < nums[high])
            return nums[low];

        while(low<=high) {
            int mid = low + (high - low)/2;
            // if current element is less than previous element
            // that means, current element is the pivot-element/min.
            if (nums[mid] < nums[mid-1]) {
              return nums[mid];
            } else if (nums[mid] > nums[high]) {
                // if current mid element is greater than last element
                // we need to search for smallest element in the second half.
                // Use the diagram in this link to understand why its so -
                // http://theoryofprogramming.com/2017/12/16/find-pivot-element-sorted-rotated-array/ 
                low = mid + 1;
            } 
            else {
                high = mid;
            }
        }

        return -1;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
