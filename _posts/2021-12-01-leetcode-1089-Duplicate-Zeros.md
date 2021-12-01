---
layout: post
title: "Leetcode 1089 : Duplicate Zeros"
date: 2021-12-01
categories: leetcode leetcode-easy Array
---

Solution to [Duplicate Zeros][leetcode] problem.

{% highlight java %}
class Solution {
    public void duplicateZeros(int[] arr) {
        int zc = 0;
        for (int i=0;i<arr.length;i++) {
            if (arr[i] == 0) zc++;
        }
        
        // This would have been the length of new array if we were not discarding the elements.
        int newLen = arr.length + zc; 
        
        // Start from back of the array and process j times.
        // Write the data to array only if j is less than n - the length of array.
        // This strategy will ensure that extra elements are discarded.
        int j = newLen - 1;
        int i = arr.length - 1;
        int n = arr.length;
        while (j>=0) {
            if (j<n) arr[j] = arr[i];
            j--;
            if (arr[i] == 0) {
                if (j<n) arr[j] = arr[i];
                j--;
            }
            i--;
        }
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/duplicate-zeros/
