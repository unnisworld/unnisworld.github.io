---
layout: post
title: "Educative Grokking : Maximum Sum Subarray of Size K"
date: 2020-07-11
categories: educative SlidingWindow
---
Maximum Sum Subarray of Size K

Problem Statement :
Given an array of positive numbers and a positive number ‘k’, find the maximum sum of any contiguous subarray of size ‘k’.

Example 1:
Input: [2, 1, 5, 1, 3, 2], k=3 
Output: 9
Explanation: Subarray with maximum sum is [5, 1, 3].

Example 2:
Input: [2, 3, 4, 1, 5], k=2 
Output: 7
Explanation: Subarray with maximum sum is [3, 4].

{% highlight java %}
class MaxSumSubArrayOfSizeK {
  public static int findMaxSumSubArray(int k, int[] arr) {
    int winStart = 0;
    int maxSum = 0, winSum = 0;
    for(int winEnd=0;winEnd<arr.length;winEnd++) {
      if(winEnd - winStart == k) {
        maxSum = Math.max(maxSum, winSum);
        winSum = winSum - arr[winStart]; // remove the outgoing element from the sum
        winStart++;
      } 
      
      winSum += arr[winEnd];
      System.out.println("Now winSum is "+ winSum);
      
    }

    return maxSum;
  }
}
{% endhighlight %}
