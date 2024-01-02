---
layout: post
title:  "Leetcode 153 : Find Minimum in rotated sorted array"
date:   2020-01-29 5:30:00 +0530
categories: leetcode-medium leetcode binarysearch array
---

Solution to [Find Minimum in Rotated Sorted Array][leetcode].

# Approach 1

Intuition : Minimum element is the first element in the array that is less than or equal to the last element in the array. Now the problem becomes a simple binary search to identify the first element that satisfy this criteria.

{% highlight java %}
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        int indexOfLastElement = nums.length - 1;
        int boundaryIndex = -1;
        while (l <= r) {
            int m = l + (r - l)/2;
            if (nums[m] <= nums[indexOfLastElement]) {
                boundaryIndex = m;
                r = m - 1;
            } else {
                l = m + 1;
            }
        }

        return nums[boundaryIndex];
    }
}
{% endhighlight %}

# Approach 2

In this approach you apply two rules during the search process.

Rule 1: If mid element is less than element at mid-1, that means mid element is the pivot element. If you think about it, the array being sorted and rotated, the pivot element is the only place a transition happens from high to low.

Rule 2: If mid element is greater than the last element in the array, then we need to search for smallest element in the second half.

While going through the code, have a look at the diagram in [this link][theoryofprogramming] to get a grasp on how we are picking the right partition during each iteration.  

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

# Approach 3

The code for approach 3 is very simple and does not require additional checks for edge case handling. This solution was given by @JJH11 in the [leetcode discussion thread][simpler-solution].

Two key rules to help understand the solution.

Rule 1: When you sort and rotate an array, you create two parts of the array, one part will be sorted and another part will be unsorted. You can determine whether a part is sorted by comparing the first and last element of that part. For ex: if nums[low] > nums[mid], that means elements from low to mid are not sorted.

Rule 2: The min element will be in the unsorted part of the sorted and rotated array.

{% highlight java %}
    public int findMin(int[] nums) {
        int low = 0, high = nums.length-1;
        while(low < high){
            int mid = (low + high) / 2;
            //check if the first half is unsorted
            if(nums[low] > nums[mid]) {
                high = mid;
            //check if the second half is unsorted
            }else if(nums[mid] > nums[high]) {
                low = mid + 1;
            }else {
                //return the first item in the remaining list
                // since now both half of the items are sorted. 
                return nums[low];
            }
        }
        
        return nums[low];
    }
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
[simpler-solution]: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/discuss/489830/very-simple-and-clean-java-solution-beats-100/439632
[theoryofprogramming]: http://theoryofprogramming.com/2017/12/16/find-pivot-element-sorted-rotated-array/
