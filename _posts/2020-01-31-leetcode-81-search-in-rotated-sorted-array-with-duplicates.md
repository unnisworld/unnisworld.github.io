---
layout: post
title:  "Leetcode : 81 Search in Rotated Sorted Array With Duplicates"
date:   2020-05-01
categories: leetcode-medium leetcode binarysearch array
---

Solution to [Search in Rotated Sorted Array With Duplicate Elements][leetcode].

# Approach 1

Approach one is a more laborious but easy to fit in head solution. It is still an O(logn) solution since it uses binary search in a 3 step process.

Intuition
A rotated sorted array will have a boundary element such that all elements before it will be > the last element of the array and all elements after it will be either <= the last element of the array. The boundary element can be found using standard binary search. Once we find the boundary element, we can do binary search on both sides of the boundary element to find check whether the element is present in the array.

Approach
Step 1 : Find the boundary element using bsearch. For this, take last element in the array as the pivot and try to locate the first element in the array that is <= the pivot.
Step 2: To handle duplicates, in step 1, during bsearch, keep skipping the left most elements while nums[l] == nums[r].
Step 3: Do bsearch on left array
Step 4: If Setp 3 did not find the element, do bsreach on right array

{% highlight java %}
class Solution {
    public boolean search(int[] nums, int target) {
        int boundaryNdx = findBoundaryElementIndex(nums);

        if (boundaryNdx == -1) {
            return false;
        }

        boolean found = bsearch(nums, 0, boundaryNdx - 1, target);

        if (!found)
            found = bsearch(nums, boundaryNdx, nums.length - 1, target);
    
        return found;
    }

    private int findBoundaryElementIndex(int[] nums) {
        int l = 0, r = nums.length - 1;
        int bNdx = r;
        
        // logic to skip duplicate elements from the left
        while (l<=r && nums[l] == nums[r]) l++;

        while(l <= r) {
            int m = l + (r -l)/2;
            if (nums[m] <= nums[nums.length - 1]) {
                bNdx = m;
                r = m - 1;
            } else {
                l = m + 1;
            }
        }

        return bNdx;
    }

    private boolean bsearch(int[] arr, int l, int r,int tgt) {
        while (l <= r) {
            int m = l + (r - l)/2;
            if (arr[m] == tgt) {
                return true;
            } else if (arr[m] > tgt) {
                r = m - 1;
            } else {
                l = m + 1;
            }
        }

        return false;
    }

}
{% endhighlight %}

# Approach 2
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
