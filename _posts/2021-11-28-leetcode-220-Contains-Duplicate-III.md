---
layout: post
title: "Leetcode 320 : Contains Duplicate III"
date: 2021-11-28
categories: leetcode leetcode-medium SlidingWindow Array
---

Solution to [Contains Duplicate III][leetcode] problem.

{% highlight java %}
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        int maxPermissibleDistance = k;
        int maxPermissibleDifference = t;
        TreeSet<Long> numsWithinMaxPermissibleDistance = new TreeSet<>(); 
        for (int i=0;i<nums.length;i++) {
            long curNum = nums[i];
            Long largestNumSmallerThanCurNum = numsWithinMaxPermissibleDistance.floor(curNum);
            Long smallestNumLargerThanCurNum = numsWithinMaxPermissibleDistance.ceiling(curNum);
            
            // You don't need to check the condition for all the numbers in the Tree Set.
            // If the floor number is not able to satisfy this condition, then none of the other numbers smaller than
            // floor num will be able to satisfy it. For eg if (6 - 5) is gt than maxPermissibleDifference then
            // (6 - 4) and (6 - 3) will obviously be greater than maxPermissibleDifference.
            if (largestNumSmallerThanCurNum != null && curNum - largestNumSmallerThanCurNum <= maxPermissibleDifference) 
            { 
                return true;
            }
            
            // Same logic applies here. If ceilNum - curNum is gt than maxPermissibleDifference then 
            // all other numbers gt than ceilNum can be skipped. If (7 - 5) is gt than maxPermissibleDifference
            // there is no need of checking (8 - 5), (9 - 5) etc.
            if (smallestNumLargerThanCurNum != null && smallestNumLargerThanCurNum - curNum <= maxPermissibleDifference) 
            {
                return true;
            }
            
            numsWithinMaxPermissibleDistance.add(curNum);
            if (numsWithinMaxPermissibleDistance.size() > maxPermissibleDistance) 
            {
                numsWithinMaxPermissibleDistance.remove((long)nums[i - maxPermissibleDistance]);
            }
        }
        
        return false;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/odd-even-linked-list/
