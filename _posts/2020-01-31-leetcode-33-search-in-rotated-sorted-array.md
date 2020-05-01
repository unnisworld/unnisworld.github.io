---
layout: post
title:  "Leetcode : 33 Search in Rotated Sorted Array"
date:   2020-02-02 8:30:00 +0530
categories: leetcode-medium leetcode binarysearch array
---

Solution to [Search in Rotated Sorted Array][leetcode].

First we will look at a solution that is built on top of the [Find Minimum Element in a rotated sorted array][find_min] problem. 

Here, first we just find the minimum element index, for example index of 0 in [5,6,7,0,1,2,3,4].
Once you identify the smallest element, then its a matter of deciding which part of the sorted array you need to perform binary search on.  

Watch this [youtube] video for a nice explanation.

{% highlight java %}
class Solution {
    public int search(int[] nums, int target) {
        if(nums == null || nums.length==0)
            return -1;
        int lo=0, hi=nums.length-1;
        
        // find min element position
        while(lo<=hi) {
            int mid = lo + (hi-lo)/2;
            if(nums[lo] > nums[mid]) { // first half is unsorted
                hi = mid;
            } else if (nums[mid] > nums[hi]) {
                lo = mid+1;
            } else {
                break;
            }
        }
        
        // found the min element Position
        int start = lo;
        if(target >= nums[start] && target <= nums[nums.length-1]) {
            hi = nums.length-1;
        } else {
            lo = 0;
            hi = start-1;
        }
        
        while(lo<=hi) {
            int mid = lo + (hi-lo)/2;
            if(nums[mid] == target) 
                return mid;
            else if(nums[mid] > target) 
                hi = mid-1;
            else
                lo = mid+1;
        }
        
        return -1;
        
    }
}
{% endhighlight %}

This is a more optimized version of the solution.

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
[find_min]: https://unnisworld.github.io/leetcode-medium/leetcode/binarysearch/2020/01/29/leetcode-153-find-min-in-rotated-sorted-array.html
[youtube]: https://www.youtube.com/watch?time_continue=542&v=QdVrY3stDD4&feature=emb_logo
