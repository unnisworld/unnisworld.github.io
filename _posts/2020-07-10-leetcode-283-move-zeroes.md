---
layout: post
title: "Leetcode 283 : Move Zeroes"
date: 2020-07-10
categories: leetcode leetcode-easy Array Sort Array-Transformation
---

Solution to [Move Zeros][leetcode] problem.

Approach 1 : Two pointer approach

{% highlight java %}
public class Solution {
    public void MoveZeroes(int[] nums) {
        int L = nums.Length;
        // Use two pointer approach
        // Traverse the array from left to right
        // mark the position of next 0 using one pointer
        // scan for the next non-zero element
        // swap zero and non-zero element
        // continue this until we reach the end of the list
        int zIndex = 0;
        int numIndex = 0;
        while(numIndex < L) {
            while(zIndex < L && nums[zIndex] != 0)
                zIndex++;
            numIndex = zIndex+1;
            
            while(numIndex < L && nums[numIndex] == 0)
                numIndex++;
            
            if(numIndex > L-1 || zIndex > L-1)
                break;
            
            nums[zIndex] = nums[numIndex];
            nums[numIndex] = 0; // IMP : set this to zero
        }

    }
}
{% endhighlight %}

Approach 2:

{% highlight java %}
public class Solution {
    public void MoveZeroes(int[] nums) {
        int insertPos = 0;
        foreach(int num in nums) {
            if(num != 0) nums[insertPos++] = num; 
        }
        
        while(insertPos < nums.Length)
            nums[insertPos++] = 0;
    }
}
{% endhighlight %}

Approach 3:
{% highlight java %}
public class Solution {
    public void MoveZeroes(int[] nums) {
        int zeroPtr = 0;
        for(int curPtr=0;curPtr<nums.Length;curPtr++) {
            if(nums[curPtr] != 0) {
                int temp = nums[curPtr];
                nums[curPtr] = nums[zeroPtr];
                nums[zeroPtr++] = temp;
            }
        }
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/move-zeroes
