---
layout: post
title:  "Leetcode 35 : Search Insert Position"
date:   2020-05-09
categories: leetcode-easy leetcode binarysearch
---

Solution to [Search Insert Position][leetcode] Problem.

{% highlight java %}
class Solution {
    
    public int searchInsert(int[] nums, int target) {
        int lo = 0; int hi = nums.length -1;
        
        int mid = -1;
        while(lo <= hi) {
            mid = lo + (hi - lo)/2;
            if(nums[mid] == target) {
                return mid;
            }
            
            if(nums[mid] < target)
                lo = mid + 1;
            
            if(nums[mid] > target)
                hi = mid - 1;
        }
        
        return lo;
}    
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/search-insert-position/