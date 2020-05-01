---
layout: post
title:  "Leetcode : 81 Search in Rotated Sorted Array With Duplicates"
date:   2020-05-01
categories: leetcode-medium leetcode binarysearch array
---

Solution to [Search in Rotated Sorted Array With Duplicate Elements][leetcode].

{% highlight java %}
class Solution {
    public boolean search(int[] nums, int target) {
        if(nums == null || nums.length == 0)
            return false;
        
        if(nums.length == 1)
            return nums[0] == target ? true : false;
        
        int lo = 0, hi = nums.length-1;
        while(lo <= hi) {
            int mid = lo + (hi - lo)/2;
            
            if(nums[mid] == target)
                return true;
            
            while(nums[lo] == nums[mid] && lo < mid)
                lo++;
            
            while(nums[hi] == nums[mid] && hi > mid)
                hi--;
            
            if(nums[lo] <= nums [mid]) { // first half is sorted
                if(target >= nums[lo] && target < nums[mid]) {
                    hi = mid - 1;
                } else {
                    lo = mid + 1;
                }
            } else { // second half is sorted
                if(target > nums[mid] && target <= nums[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            }
        }
        
        return false;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/search-in-rotated-sorted-array-ii/
