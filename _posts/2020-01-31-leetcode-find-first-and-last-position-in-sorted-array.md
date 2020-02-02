---
layout: post
title:  "Find First and Last Position of Element in Sorted Array"
date:   2020-01-29 5:30:00 +0530
categories: leetcode-medium leetcode binarysearch
---

Solution to [Find First and Last Position of Element in Sorted Array][leetcode].

While going through the code, have a look at the diagram in [this link][theoryofprogramming] to get a grasp on how we are picking the right partition during each iteration.  

{% highlight java %}
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int startNdx = -1;
        int endNdx = -1;
        int l=0, r = nums.length-1;
        while(l<=r) {
            int m=l + (r-l)/2;
            if (nums[m] == target) {
                startNdx = m;
                endNdx = m;
                while(startNdx>=l && nums[startNdx] == target) {
                    startNdx--;    
                }
                startNdx++;
                while(endNdx<=r && nums[endNdx] == target) {
                    endNdx++;    
                }
                endNdx--;
                return new int[] {startNdx, endNdx};
            } else if (nums[m] < target) {
                l=m+1;
            } else {
                r = m-1;
            }
        }
        
        return new int[] {-1, -1};
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
