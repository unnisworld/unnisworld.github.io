---
layout: post
title:  "Leetcode : 75 Sort Colors"
date:   2020-05-01
categories: leetcode-medium leetcode sort array
---

Solution to [Sort Colors][leetcode] Problem. This [video][video] will help you understand the Solution better.

{% highlight java %}
class Solution {
    
    public void sortColors(int[] nums) {
        int start=0,end=nums.length-1;
        int index = 0;
        
        while(index <= end) {
            if(nums[index] == 0) {
                nums[index] = nums[start];
                nums[start] = 0;
                index++; start++;
            } else if (nums[index] == 2) {
                nums[index] = nums[end];
                nums[end] = 2;
                end--;
            } else {
                index++;
            }
        }

    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/sort-colors/
[video]: https://www.youtube.com/watch?v=uvB-Ns_TVis
