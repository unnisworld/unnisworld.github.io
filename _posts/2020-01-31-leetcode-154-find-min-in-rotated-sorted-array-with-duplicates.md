---
layout: post
title:  "Leetcode 154 : Find Minimum in rotated sorted array with duplicates"
date:   2020-01-29 5:30:00 +0530
categories: leetcode-medium leetcode binarysearch array
---

Solution to [Find Minimum in Rotated Sorted Array with possible duplicate elements][leetcode].

# Approach 1
# Intuition 
Minimum element is the first element in the array that is less than or equal to the last element in the array. Now the problem becomes a simple binary search to identify the first element that satisfy this criteria. The only additional trick is to add some code to handle the duplicate elements. For this, we will keep skipping duplicate elements from the left that are equal to the pivot (last element).

# Approach
1. Take last element as the Pivot element.
2. Skip duplicate Pivot elements from the left. Duplicate pivot elements are those elements from the left of the array that are equal to the last element of the array.
3. Now do binary search on the array to find the first element that is less than or equal to the last element.

{% highlight java %}
class Solution {
    public int findMin(int[] nums) {
        int l = 0, r = nums.length - 1;
        int boundaryElementIndex = r;
        while( l <= r && nums[l] == nums[r]) { l++;}

        while (l <= r) {
            int m = l + (r - l)/2;
            if (nums[m] <= nums[nums.length-1]) {
                boundaryElementIndex = m;
                r = m - 1;
            } else {
                l = m + 1;
            }
        }

        return nums[boundaryElementIndex];
    }
}
{% endhighlight %}

# Approach 2

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
            int mid = low + (high-low)/2;

            // Skip duplicates (if any) from the right side.
            while(high>mid && nums[mid] == nums[high])
                high = high - 1;

            // if (mid == 0) is required to handle array with only duplicate entries. eg: {1,1,1}.
            // if current element is less than previous element
            // that means, current element is the pivot-element/min.
            if (mid == 0 || nums[mid] < nums[mid-1]) {
              return nums[mid];
            }
            // if current mid element is greater than last element
            // we need to search for smallest element in the second half.
            // Use the diagram in this link to understand why its so -
            // http://theoryofprogramming.com/2017/12/16/find-pivot-element-sorted-rotated-array/
            else if (nums[mid] > nums[high]) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }

        return -1;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/
[theoryofprogramming]: http://theoryofprogramming.com/2017/12/16/find-pivot-element-sorted-rotated-array/
