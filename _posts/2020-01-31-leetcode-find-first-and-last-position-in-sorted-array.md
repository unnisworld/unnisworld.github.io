---
layout: post
title:  "Leetcode 34. Find First and Last Position of Element in Sorted Array"
date:   2020-01-29 5:30:00 +0530
categories: leetcode-medium leetcode binarysearch
---

Solution to [Find First and Last Position of Element in Sorted Array][leetcode].

The first approach uses two binary searches to find the first and last index of target element. 
{% highlight java %}
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if (nums == null || nums.length == 0) return new int[] {-1, -1};
        
        int li = findLeftIndex(nums, target);
        
        if (li == -1) return new int[] {-1, -1};
        
        int ri = findRightIndex(nums, target);
        
        return new int[] {li, ri};
    }
    
    private int findLeftIndex(int[] nums, int t) {
        int li = -1;
        int l = 0, r = nums.length - 1;
        
        while (l <= r) {
            int m = l + (r - l)/2;
            
            if (nums[m] > t) {
                r = m - 1;
            }
            else if (nums[m] < t) {
                l = m + 1;
            }
            else {
                li = m; // save the one that we found
                r = m - 1; // now look for better left index
            }
        }
        
        return li;
    }
    
    private int findRightIndex(int[] nums, int t) {
        int ri = -1;
        int l = 0, r = nums.length - 1;
        
        while (l <= r) {
            int m = l + (r - l)/2;
            
            if (nums[m] > t) {
                r = m - 1;
            } else if (nums[m] < t) {
                l = m + 1;
            } else {
                ri = m; // save this index
                l = m + 1; // look for better index
            }
        }
        
        return ri;
    }
}
{% endhighlight %}

The second approach tries to find the index of any one occurance of the target element and then tries to expand the range. 

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
