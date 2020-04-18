---
layout: post
title:  "Leetcode 697 : Degree of an Array"
date:   2020-04-18
categories: leetcode leetcode-easy Array
---

Solution to [Degree of an Array][leetcode] problem.


{% highlight java %}
class Solution {
    public int findShortestSubArray(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        
        // Build frequency map
        Map<Integer, int[]> fm = new HashMap<>();
        for(int i=0;i<nums.length;i++) {
            if(!fm.containsKey(nums[i])) {
                fm.put(nums[i], new int[] {1, i, i});
            } else {
                int[] t = fm.get(nums[i]);
                t[0]++;
                t[2] = i;
            }
        }
        
        int maxFreq = 0;
        int minLen = Integer.MAX_VALUE;
        for(int[] f : fm.values()) {
            if (f[0] > maxFreq) {
                minLen = f[2] - f[1];
                maxFreq = f[0];
            } else if(f[0] == maxFreq) {
                minLen = Math.min(minLen, (f[2] - f[1]));
            }
        }
        
        return minLen + 1;
    }
}
{% endhighlight %}

[leetcode]: https://leetcode.com/problems/degree-of-an-array/
